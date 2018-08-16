##Url Parser
    Parse a html page, extract the Urls in it.

    Hint: use regex to parse html.

##Example
    Given the following html page:

    <html>
      <body>
        <div>
          <a href="http://www.google.com" class="text-lg">Google</a>
          <a href="http://www.facebook.com" style="display:none">Facebook</a>
        </div>
        <div>
          <a href="https://www.linkedin.com">Linkedin</a>
          <a href = "http://github.io">LintCode</a>
        </div>
      </body>
    </html>
    You should return the Urls in it:

    [
      "http://www.google.com",
      "http://www.facebook.com",
      "https://www.linkedin.com",
      "http://github.io"
    ]




##思路
- 我的思路先拆分，找出href后的字符串，再找url
- 代码如下，能通过70%，但是有extreme case没通过

```java
public class HtmlParser {

    public List<String> parseUrls(String content) {
        // write your code here
        List<String> results = new ArrayList<String>();
        String[] array = content.split("(?i)href[\\s]*=[\\s]*\\\"");


        for (int i = 1; i < array.length; i++) {
            String s = array[i];
            System.out.println(s + "||||");
            int index = s.indexOf("\"");
            if (index != -1 && s.charAt(0) != '#') {
                String url = s.substring(0, index);
                if (!url.equals("")) {
                    results.add(url);
                }
            }
        }

        return results;
    }
}
```

###正确解法

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;


public class HtmlParser {
    private static final String HTML_HREF_TAG_PATTERN =  "\\s*(?i)href\\s*=\\s*(\"|')+([^\"'>\\s]*)";
    /**
     * @param content source code
     * @return a list of links
     */
    public List<String> parseUrls(String content) {
        // Write your code here
        List<String> links = new ArrayList<String>();
        Pattern pattern = Pattern.compile(HTML_HREF_TAG_PATTERN, Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(content);
        String url = null;
        while (matcher.find()) {
            url = matcher.group(2);
            if (url.length() == 0 || url.startsWith("#"))
                continue;
            links.add(url);
        }
        return links;
    }
}
```
