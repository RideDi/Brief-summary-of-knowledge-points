# LK 刷题

## 二叉树

144前序遍历	递归+迭代

94中序遍历	  递归+迭代

145后序遍历	递归	**迭代**

------

468 验证IP地址

```java
class Solution {
    public String validIPAddress(String IP) {
        if(IP.chars().filter(ch -> ch == '.').count() == 3) {
            return validIPv4Address(IP);
        }else if(IP.chars().filter(ch -> ch == ':').count() == 7) {
            return validIPv6Address(IP);
        }
        return "Neither";
    }
    private String validIPv4Address(String IP) {
        String[] nums = IP.split("\\.",-1);//-1是没有东西的时候
        /*
            判断需要顺序
                先判断长度，单个字符长度0或>3
                再判断前导0的情况，只有第一位是0且长度不是1的情况，违法
                如果127.0.0.1是合法的
                然后判断每个部分的数字大小，<255是合法，0已经判断过了
        */
        for(String x : nums) {
            if(x.length() == 0 || x.length() > 3)
                return "Neither";
            if(x.charAt(0) == '0' && x.length() != 1)
                return "Neither";
            for(char ch : x.toCharArray()){
                if(!Character.isDigit(ch))
                    return "Neither";
            }
            if(Integer.valueOf(x) > 255)
                return "Neither";
        }
        return "IPv4";
    }
    private String validIPv6Address(String IP) {
        String[] nums = IP.split(":",-1);
        String allAllowedNum = "0123456789aAbBcCdDeEfF";
        for(String x : nums) {
            if(x.length() == 0 || x.length() > 4)
                return "Neither";
            for(char ch : x.toCharArray()) {
                if(allAllowedNum.indexOf(ch) == -1)
                    return "Neither";
            }
        }
        return "IPv6";
    }
}
```

```jav
import java.util.regex.Pattern;
class Solution {
    String chunkedIPv4 = "([0-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])";
    String chunkedIPv6 = "([0-9a-fA-F]{1,4})";
    //Pattern patternv4 = Pattern.compile("^(" + chunkedIPv4 + "\\.{3}" + chunkedIPv4 + "$"); 
    Pattern pattenIPv4 = Pattern.compile("^(" + chunkedIPv4 + "\\.){3}" + chunkedIPv4 + "$");
    Pattern patternv6 = Pattern.compile("^(" + chunkedIPv6 + "\\:){7}" + chunkedIPv6 + "$");
    public String validIPAddress(String IP) {
        if(IP.contains(".")){
            return (pattenIPv4.matcher(IP).matches()) ? "IPv4" : "Neither";
        }else if(IP.contains(":")){
            return (patternv6.matcher(IP).matches()) ? "IPv6" : "Neither";
        }
        return "Neither";
    }   
}
```

