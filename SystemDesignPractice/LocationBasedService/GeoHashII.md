###GeoHash II

##Description
This is a followup question for Geohash.

Convert a Geohash string to latitude and longitude.

Try http://geohash.co/.

Check how to generate geohash on wiki: Geohash or just google it for more details.


##Example
Given "wx4g0s", return lat = 39.92706299 and lng = 116.39465332.

Return double[2], first double is latitude and second double is longitude.

##思路
- 思路不难,跟geohash反其道而行之,所以我设置了一个range的参数,然后每次减半
- 但是我的代码没办法通过,也没找出来原因

##我的代码

```java
public double[] decode(String geohash) {
        // write your code here
        double[] location = new double[2];

        double lon = 0;
        double lat = 0;
        double range = 180;

        for (int i = 0; i < geohash.length(); i++) {

            int minIndex = 0;
            int maxIndex = base32.length() - 1;
            int divideTimes = 0;
            boolean eventLon = true;
            int curLocation = base32.indexOf(geohash.charAt(i));
            range = range / 2;
            while(divideTimes != 5) {
                int mid = (minIndex + maxIndex) / 2;
                if (eventLon) {
                    if (mid >= curLocation) {
                        maxIndex = mid;
                        lon = lon - range;
                    } else {
                        minIndex = mid;
                        lon = lon + range;
                    }
                    range = range / 2;
                } else {
                    if (mid >= curLocation) {
                        maxIndex = mid;
                        lat = lat - range;
                    } else {
                        minIndex = mid;
                        lat = lat + range;
                    }
                }
                eventLon = !eventLon;
                divideTimes++;
            }
        }

        location[0] = lat;
        location[1] = lon;
        return location;
    }
```

##正确答案
```java
public class GeoHash {

    String base32 = "0123456789bcdefghjkmnpqrstuvwxyz";

    public double[] decode(String geohash) {
        // Write your code here
        String _base32 = "0123456789bcdefghjkmnpqrstuvwxyz";
        int[] mask = {16, 8, 4, 2, 1};
        double[] lon = {-180, 180};
        double[] lat = {-90, 90};
        boolean is_even = true;

        for (int i = 0; i < geohash.length(); ++i) {
            int val = _base32.indexOf(geohash.charAt(i));
            for (int j = 0; j < 5; ++j) {
                if (is_even) {
                    refine_interval(lon, val, mask[j]);
                } else {
                    refine_interval(lat, val, mask[j]);
                }
                is_even = ! is_even;
            }
        }
        double[] location = {(lat[0] + lat[1]) / 2.0, (lon[0] + lon[1]) / 2.0};
        return location;
    }

    public void refine_interval(double[] interval, int val, int mask) {
        if ((val & mask) > 0) {
            interval[0] = (interval[0] + interval[1]) / 2.0;
        } else {
            interval[1] = (interval[0] + interval[1]) / 2.0;
        }
    }

}
```
