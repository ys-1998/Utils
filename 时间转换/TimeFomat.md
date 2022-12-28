# 时间转换

## date =>string

```
 		Date createTime = video1.getCreateTime();//从数据库中获取到了Date类型的时间
        SimpleDateFormat simpleDateFormat=new SimpleDateFormat("yyyy:MM:dd HH:mm:ss");
        String format = simpleDateFormat.format(createTime);
```

## LocalDateTime =>String

```
	 LocalDateTime localDateTime=LocalDateTime.now();
        String format1 = localDateTime.format(DateTimeFormatter.ofPattern("yyyy:MM:dd HH:mm:ss"));
```



## String =>LocalDateTime(2048-12-12T12:12:12)

```
 		String time="2048-12-12 12-12-12";
        LocalDateTime parse = LocalDateTime.parse(time, DateTimeFormatter.ofPattern("yyyy-MM-dd HH-mm-ss"));
```



## String =>Date(Sat Dec 12 12:12:12 CST 2048)

```
Date date=null;
        try {
            String time2="2048-12-12 12-12-12";
            date= new SimpleDateFormat("yyyy-MM-dd HH-mm-ss").parse(time2);
        } catch (ParseException e) {
            e.printStackTrace();
        }
```

## 格式时间2022-12-01 00：00：00 转换时间戳格式

```
public class TimeUtil {

    public static long timeToStamp(String times){
        SimpleDateFormat simpleDateFormat=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String mytime=times;
        try {
            Date parse = simpleDateFormat.parse(mytime);
            long time = parse.getTime();
            return time;
        } catch (ParseException e) {
            e.printStackTrace();
        }

        return -1;
    }
}
```

