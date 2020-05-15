# graylog_extractors
Some Graylog extractors  

### palo alto

The Palo Alto logger for TRAFFIC  can be configured to log in JSON Format.
Take care to the key "type".  Its reseverd in Graylog.

    { "log_type":"$type", "action":"$action", "app":"$app", "category":"$category", "direction":"$direction", "dstPort":"$dport", "dstIP":"$dst", "dstGeo":"$dstloc", "inbound_if":"$inbound_if", "natDstPort":"$natdport", "natDst":"$natdst", "natSrcPort":"$natsport", "natSrc":"$natsrc", "outbound_if":"$outbound_if", "protocol":"$proto", "recipient":"$recipient", "repeatcount":"$repeatcnt", "rule":"$rule", "sender":"$sender", "severity":"$severity", "srcPort":"$sport", "srcIP":"$src", "time_generated":"$time_generated", "byte":"$bytes", "bytes_received":"$bytes_received", "bytes_sent":"$bytes_sent", "session_end_reason":"$session_end_reason" }

If you find your message in field "message" you can use extractor_type **json** and adjust the timsstamp field.

``` 
{
  "extractors": [
    {
      "title": "json_message",
      "extractor_type": "json",
      "converters": [],
      "order": 0,
      "cursor_strategy": "copy",
      "source_field": "message",
      "target_field": "",
      "extractor_config": {
        "list_separator": ", ",
        "kv_separator": "=",
        "key_prefix": "",
        "key_separator": "_",
        "replace_key_whitespace": false,
        "key_whitespace_replacement": "_"
      },
      "condition_type": "none",
      "condition_value": ""
    },
    {
      "title": "time_generated",
      "extractor_type": "copy_input",
      "converters": [
        {
          "type": "date",
          "config": {
            "date_format": "yyyy/MM/dd HH:mm:ss",
            "time_zone": "Europe/Berlin",
            "locale": "und"
          }
        }
      ],
      "order": 0,
      "cursor_strategy": "copy",
      "source_field": "time_generated",
      "target_field": "timestamp",
      "extractor_config": {},
      "condition_type": "none",
      "condition_value": ""
    }
  ],
  "version": "3.1.3"
}
```
