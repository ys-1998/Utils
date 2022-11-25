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


