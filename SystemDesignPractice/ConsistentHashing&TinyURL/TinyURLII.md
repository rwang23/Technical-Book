##Tiny Url II
[Lintcode](https://www.lintcode.com/problem/tiny-url-ii/description)


##Description
As a follow up for Tiny URL, we are going to support custom tiny url, so that user can create their own tiny url.

Custom url may have more than 6 characters in path.

##Example
	createCustom("http://www.lintcode.com/", "lccode")
	>> http://tiny.url/lccode
	createCustom("http://www.lintcode.com/", "lc")
	>> error
	longToShort("http://www.lintcode.com/problem/")
	>> http://tiny.url/1Ab38c   // this is just an example, you can have you own 6 characters.
	shortToLong("http://tiny.url/lccode")
	>> http://www.lintcode.com/
	shortToLong("http://tiny.url/1Ab38c")
	>> http://www.lintcode.com/problem/
	shortToLong("http://tiny.url/1Ab38d")
	>> null

##思路
- 在I上加入两个map,进行存储custome to url 和 Url to custome
- 并且每次查找long to short 和 short to long的时候,优先查找custom这两个map

```java
public class TinyUrl2 {
    public static int GLOBAL_ID = 0;
    private HashMap<Integer, String> id2url = new HashMap<Integer, String>();
    private HashMap<String, Integer> url2id = new HashMap<String, Integer>();
    private HashMap<String, String> url2custom = new HashMap<String, String>();
    private HashMap<String, String> custom2url = new HashMap<String, String>();

    private String getShortKey(String url) {
        return url.substring("http://tiny.url/".length());
    }

    private int toBase62(char c) {
        if (c >= '0' && c <= '9') {
            return c - '0';
        }
        if (c >= 'a' && c <= 'z') {
            return c - 'a' + 10;
        }
        return c - 'A' + 36;
    }

    private int shortKeytoID(String short_key) {
        int id = 0;
        for (int i = 0; i < short_key.length(); ++i) {
            id = id * 62 + toBase62(short_key.charAt(i));
        }
        return id;
    }

    private String idToShortKey(int id) {
        String chars = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String short_url = "";

        if (id == 0) {
            return new String("000000");
        }
        while (id > 0) {
            short_url = chars.charAt(id % 62) + short_url;
            id = id / 62;
        }
        while (short_url.length() < 6) {
            short_url = "0" + short_url;
        }
        return short_url;
    }

    /*
     * @param long_url: a long url
     * @param key: a short key
     * @return: a short url starts with http://tiny.url/
     */
    public String createCustom(String long_url, String key) {
        // write your code here
        int id = shortKeytoID(key);
        if (id2url.containsKey(id)) {
            if (id2url.get(id).equals(long_url)) {
                return "http://tiny.url/" + key;
            } else {
                return new String("error");
            }
        }

        if (url2custom.containsKey(long_url)) {
            if (url2custom.get(long_url).equals(key)) {
                return "http://tiny.url/" + key;
            } else {
                return new String("error");
            }
        }

        if (custom2url.containsKey(key)) {
            return new String("error");
        }
        url2custom.put(long_url, key);
        custom2url.put(key, long_url);

        return "http://tiny.url/" + key;

    }

    /**
     * @param url a long url
     * @return a short url starts with http://tiny.url/
     */
    public String longToShort(String url) {
        if (url2custom.containsKey(url)) {
            return "http://tiny.url/" + url2custom.get(url);
        }

        if (url2id.containsKey(url)) {
            return "http://tiny.url/" + idToShortKey(url2id.get(url));
        }

        while (true) {
            String shortURL = idToShortKey(GLOBAL_ID);
            if (custom2url.containsKey(shortURL)) {
                GLOBAL_ID++;
            } else {
                break;
            }
        }
        url2id.put(url, GLOBAL_ID);
        id2url.put(GLOBAL_ID, url);
        return "http://tiny.url/" + idToShortKey(GLOBAL_ID++);
    }

    /**
     * @param url a short url starts with http://tiny.url/
     * @return a long url
     */
    public String shortToLong(String url) {
        String realURL = url.substring("http://tiny.url/".length());
        if (custom2url.containsKey(realURL)) {
            return custom2url.get(realURL);
        }

        String short_key = getShortKey(url);
        int id = shortKeytoID(short_key);
        return id2url.get(id);
    }
}
```
