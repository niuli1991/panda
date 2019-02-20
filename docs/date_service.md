##时间日期工具类方法

``` java
    public String plusDays(Date targetDate, int amount) {
        SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd");
        logger.debug("目标日期 {}", targetDate);
        Date newDate = new Date(targetDate.getTime()+(1000 * 60 *60 *24 *amount));
        logger.debug("目标日期加一天 {}", sdf.format(newDate));
        return sdf.format(newDate);
    }
    public Date getYesterday() {
        Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DATE, -1);
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
        return cal.getTime();
    }
    public Date atStartOfDay(Date date) {
        LocalDateTime localDateTime = dateToLocalDateTime(date);
        LocalDateTime startOfDay = localDateTime.with(LocalTime.MIN);
        return localDateTimeToDate(startOfDay);
    }

    public Date atEndOfDay(Date date) {
        LocalDateTime localDateTime = dateToLocalDateTime(date);
        LocalDateTime endOfDay = localDateTime.with(LocalTime.MAX);
        return localDateTimeToDate(endOfDay);
    }
    public Date atEndOfMonth(String date) {
        LocalDate converedDate = LocalDate.parse(date, DateTimeFormatter.ofPattern("yyyy-M-d"));
        converedDate = converedDate.withDayOfMonth(converedDate.getMonth().length(converedDate.isLeapYear()));
        return Date.from(converedDate.atStartOfDay().atZone(ZoneId.systemDefault()).toInstant());
    }
    public Date atStartOfMonth(Date date) {
        Calendar cal = Calendar.getInstance();
        cal.setTime(date);
        cal.set(Calendar.DAY_OF_MONTH, cal.getActualMinimum(Calendar.DAY_OF_MONTH));
        return cal.getTime();
    }
    public int lenthOfMonth(String date) {
        LocalDate converedDate = LocalDate.parse(date, DateTimeFormatter.ofPattern("yyyy-M-d"));
        return converedDate.lengthOfMonth();
    }
    public Date getLastMonthDate(Date date) {
        return localDateTimeToDate(dateToLocalDateTime(date).minusMonths(1));
    }
    private LocalDateTime dateToLocalDateTime(Date date) {
        return LocalDateTime.ofInstant(date.toInstant(), ZoneId.systemDefault());
    }
    private static Date localDateTimeToDate(LocalDateTime localDateTime) {
        return Date.from(localDateTime.atZone(ZoneId.systemDefault()).toInstant());
    }
```
