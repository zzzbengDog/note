# URL匹配AntPathMatcher

- ant风格匹配规则

  | 字符 | 描述              |
  | :--- | ----------------- |
  | ?    | 匹配一个字符      |
  | *    | 匹配0个及以上字符 |
  | **   | 匹配0个及以上目录 |

  

- PathMatcher接口

  ```java
  public interface PathMatcher {
      //最重要的方法。判断path和模式pattern是否匹配。patten:ant风格url。
  	boolean match(String pattern, String path);
  	//判断path是否是一个模式字符串（一般含有指定风格的特殊通配符就算是模式了）
  	boolean isPattern(String path);	
      //判断path是否和模式pattern前缀匹配（前缀匹配：path的前缀匹配上patter了即可，当然全部匹配也是可以的）
  	boolean matchStart(String pattern, String path);
  	//返回和pattern模式真正匹配上的那部分字符串。举例：/api/yourbatman/*.html为pattern，/api/yourbatman/form.html为path，那么该方法返回结	  果为form.html（注意：返回结果永远不为null，可能是空串）	
  	String extractPathWithinPattern(String pattern, String path);
      //提取path中模板变量。举例：/api/yourbatman/{age}为pattern，/api/yourbatman/18为path，那么该方法返回结果为Map值为{"age" : 18}
  	Map<String, String> extractUriTemplateVariables(String pattern, String path);
      //路径比较器，用于排序确定优先级高低
  	Comparator<String> getPatternComparator(String path);
      //合并两个pattern模式，组合算法由具体实现自由决定
  	String combine(String pattern1, String pattern2);
  }
  ```

  

