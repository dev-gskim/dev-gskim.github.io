# influxdb, telegraf 설치

influxData 가 기본 site 이다.

최신 버전의 Download 는 : [https://portal.influxdata.com/downloads/](https://portal.influxdata.com/downloads/) 에서 받으면 된다.

## influxdb

아래 설명은 binary 설치파일\(2019.12\) 기준으로 작성하였습니다.

### Install

* binary file을 이용한 install

  ```bash
  wget https://dl.influxdata.com/influxdb/releases/influxdb-1.7.9_linux_amd64.tar.gz
  ```

* tar 명령어로 압축해제

  ```bash
  tar -zxvf influxdb-1.7.9_linux_amd64.tar.gz
  ```

### config

default 설정 사용 execute

* start.sh 작성

  ```bash
  cd /home/bkryu/influxdb-1.7.9-1/usr/bin/
  ./influxd &
  ```

* start.sh 실행권한 부여

  ```bash
  chmod 711 start.sh
  ```

* start.sh 실행

  ```bash
  ./start.sh
  ```

### process exit

* stop.sh 작성

  ```bash
  PID=`pidof telegraf`
  kill -9 ${PID}
  ```

* stop.sh 실행권한 부여

  ```bash
  chmod 711 stop.sh
  ```

* stop.sh 실행

  ```bash
  ./stop.sh
  ```

## telegraf

아래 설명은 binary 설치파일 기준으로 작성하였습니다.

### install

* binary file을 이용한 install

```bash
wget https://dl.influxdata.com/telegraf/releases/telegraf-1.13.0_linux_amd64.tar.gz
```

* tar 명령어로 압축해제

  ```bash
  tar -zxvf telegraf-1.13.0_linux_amd64.tar.gz
  ```

### modify telegraf configuration

* telegraf 설정 파일 경로

  ```bash
  $TELEGRAF_HOME/etc/telegraf/telegraf.conf
  ```

* vim 편집기로 설정파일 수정

  ```bash
  vim telegraf.conf
  ```

### input plugin 설정

* input tail plugin 설정

  ```bash
  [[inputs.tail]]
    ## files to tail.
    ## These accept standard unix glob matching rules, but with the addition of
    ## ** as a "super asterisk". ie:
    ##   "/var/log/**.log"  -> recursively find all .log files in /var/log
    ##   "/var/log/*/*.log" -> find all .log files with a parent dir in /var/log
    ##   "/var/log/apache.log" -> just tail the apache log file
    ##
    ## See https://github.com/gobwas/glob for more examples
    ##
    ##files = ["/var/mymetrics.out"]
    files = ["/home/bkryu/upload/example2.csv"]
    ## Read file from beginning.
    from_beginning = true
    ## Whether file is a named pipe
    ##pipe = false
    pipe = false

    ## Method used to watch for file updates.  Can be either "inotify" or "poll".
    ## watch_method = "inotify"

    ## Data format to consume.
    ## Each data format has its own unique set of configuration options, read
    ## more about them here:
    ## https://github.com/influxdata/telegraf/blob/master/docs/DATA_FORMATS_INPUT.md
    data_format = "csv"
    ## Indicates how many rows to treat as a header. By default, the parser assumes
    ## there is no header and will parse the first row as data. If set to anything more
    ## than 1, column names will be concatenated with the name listed in the next header row.
    ## If `csv_column_names` is specified, the column names in header will be overridden.
    csv_header_row_count = 1

    ## For assigning custom names to columns
    ## If this is specified, all columns should have a name
    ## Unnamed columns will be ignored by the parser.
    ## If `csv_header_row_count` is set to 0, this config must be used
    ##   csv_column_names = []

    ## For assigning explicit data types to columns.
    ## Supported types: "int", "float", "bool", "string".
    ## Specify types in order by column (e.g. `["string", "int", "float"]`)
    ## If this is not specified, type conversion will be done on the types above.
    csv_column_types = []

    ## Indicates the number of rows to skip before looking for header information.
    csv_skip_rows = 0
    ## Indicates the number of columns to skip before looking for data to parse.
    ## These columns will be skipped in the header as well.
    csv_skip_columns = 0

    ## The seperator between csv fields
    ## By default, the parser assumes a comma (",")
    csv_delimiter = ","

    ## The character reserved for marking a row as a comment row
    ## Commented rows are skipped and not parsed
    csv_comment = ""

    ## If set to true, the parser will remove leading whitespace from fields
    ## By default, this is false
    csv_trim_space = false

    ## Columns listed here will be added as tags. Any other columns
    ## will be added as fields.
    csv_tag_columns = ["evt_seq"]

    ## The column to extract the name of the metric from
    csv_measurement_column = "measurement"

    ## The column to extract time information for the metric
    ## `csv_timestamp_format` must be specified if this is used
    csv_timestamp_column = "actn_dt"

    ## The format of time data extracted from `csv_timestamp_column`
    ## this must be specified if `csv_timestamp_column` is specified
    csv_timestamp_format = "unix_ns"
  ```

### output plugin 설정

* output influxdb plugin 설정

  ```bash
  [[outputs.influxdb]]
  ## The full HTTP or UDP URL for your InfluxDB instance.
  ##
  ## Multiple URLs can be specified for a single cluster, only ONE of the
  ## urls will be written to each interval.
  # urls = ["unix:///var/run/influxdb.sock"]
  # urls = ["udp://127.0.0.1:8089"]
  urls = ["http://127.0.0.1:8086"] # influxdb의 default port가 8086

  ## The target database for metrics; will be created as needed.
  ## For UDP url endpoint database needs to be configured on server side.
  # database = "telegraf" # database 이름
  ```

* output file plugin 설정

  ```bash
  [[outputs.file]]
    ## Files to write to, "stdout" is a specially handled file.
    files = ["stdout", "/home/bkryu/download/metrics.json"] – output 파일명
    ## Use batch serialization format instead of line based delimiting.  The
    ## batch format allows for the production of non line based output formats and
    ## may more effiently encode metric groups.
    # use_batch_format = false
    use_batch_format = false
    ## The file will be rotated after the time interval specified.  When set
    ## to 0 no time based rotation is performed.
    # rotation_interval = "0d"
    rotation_interval = "0d"
    rotation_interval = "10s" # input을 10초 단위로 쪼개 파일 생성
    ## The logfile will be rotated when it becomes larger than the specified
    ## size.  When set to 0 no size based rotation is performed.
    # rotation_max_size = "0MB" # input을 file 용량 단위로 쪼개 파일 생성
    ## Maximum number of rotated archives to keep, any older logs are deleted.
    ## If set to -1, no archives are removed.
    # rotation_max_archives = 5
    rotation_max_archives = 5 # 최대 파일 수(이 숫자를 초과하여 파일 생성시 기존 파일 삭제됨)
    ## Data format to output.
    ## Each data format has its own unique set of configuration options, read
    ## more about them here:
    ## https://github.com/influxdata/telegraf/blob/master/docs/DATA_FORMATS_OUTPUT.md
    # data_format = "influx"
    data_format = "json" # format은 Carbon2, Graphite, InfluxDB Line Protocol, JSON, ServiceNow Metrics, SplunkMetric 만 가능
    ## The resolution to use for the metric timestamp.  Must be a duration string
    ## such as "1ns", "1us", "1ms", "10ms", "1s".  Durations are truncated to
    ## the power of 10 less than the specified units.
    json_timestamp_units = "1s"
  ```

### execute

* telegraf 폴더 아래 start.sh 파일 생성

  ```bash
  # start.sh
  cd telegraf폴더/usr/bin
  ./telegraf --config telegref폴더/etc/telegraf/telegraf.conf &
  ```

* start.sh 실행권한 부여

  ```bash
  chmod 711 start.sh
  ```

* start.sh 실행

  ```bash
  ./start.sh
  ```

### process exit

* telegraf 폴더 아래 stop.sh 파일 생성

  ```bash
  PID=`pidof telegraf`
  kill -9 ${PID}
  ```

* stop.sh 실행권한 부여

  ```bash
  chmod 711 stop.sh
  ```

* telegraf 프로세스 종료

  ```bash
  ./stop.sh
  ```

## CSV file

### 형식

* 예제 - example.csv\(/home/bkryu/upload/eample.csv\)

  ```bash
  measurement,evt_seq,actn_dt,occu_dtl,actn_dtl,actnr,cretr
  evt_hist,1140,1554808929000000000,통신불량으로 추측,정지,홍길동,admin
  evt_hist,1138,1554841353000000000,통신불량으로 추측,정지,홍길동,admin
  evt_hist,1136,1554841739000000000,통신 문제,정지,홍길동,admin
  evt_hist,1139,1554841162000000000,원인불명,조치함,홍길동,admin
  evt_hist,1159,1556568390000000000,통신불량으로 추측,정지,홍길동,admin
  evt_hist,1161,1556575556000000000,한전 정전,한전 정전,홍길동,admin
  evt_hist,1160,1556576287000000000,정전,서비스기동,홍길동,admin
  evt_hist,1158,1556578942000000000,정전,서비스 재기동,홍길동,admin
  evt_hist,1154,1556579393000000000,정전,서비스 재기동,홍길동,admin
  evt_hist,1162,1556579502000000000,정전,서비스 재기동,홍길동,admin
  evt_hist,1152,1556579695000000000,정전,서비스 재기동,홍길동,admin
  evt_hist,1145,1556589295000000000,정전,서비스 재기동,홍길동,admin
  evt_hist,1213,1556590448000000000,정전,서비스 재기동,홍길동,admin
  evt_hist,1216,1556653282000000000,통신불량으로 추측,수정된 거 테스트 중인데... 사이트명과 이벤트명을 조치내역과 함께 넣어주세요,이순신,admin
  ```



