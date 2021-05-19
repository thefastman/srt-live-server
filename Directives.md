Directives
description for config file.

# 1.srt
  ## **worker_threads**
  worker threads for sls, it is recommended than threads match the count of cpu core.
  
  ## worker_connections
  the max client connection for each worker thread, please set this value according the cpu ability ;

  ## log_file
  log file name, such as logs/error.log ; 
    
  ## log_level 
  log level, include trace, debug, info, warning, error and fatal;
    
  ## stat_post_url 
  statistic info url, sls will post the statistic info with it. example: http://192.168.31.106:8001/sls/stat;

  ## stat_post_interval 
  the interval of posting the statistic info to server, unit s.

  ## record_hls_path_prefix 
  the prefix of record hls, example: /tmp/mov/sls;
  the full record path is: /tmp/mov/sls/$listen/$domain_publisher/$app_publisher/$stream_name
  the default vod record filename is: /tmp/mov/sls/$listen/$domain_publisher/$app_publisher/$stream_name/vod.m3u8
  when publisher stop, the vod record file will be generated.

# 2.server
  ## listen
  the sls listen port. 

  ## backlog
  accept connections at the same time
        
  ## latency 
  the net latency of srt. unit:ms

  ## domain_player 
  the play url domain name which can be more than one, divided by space , example: live.sls.com live-1.sls.com;
  
  ## domain_publisher 
  the publish url domain name witch mast be single. example: uplive.sls.com;
        
  ## idle_streams_timeout
  the timeout of no data, when timeout the server will discard the client. unit s, -1 is unlimited, for player and publisher.  
 
  ## on_event_url
  the sls post the on_connect and on_close event to the http manager server, the syntax of the post url is like:  
  http://192.168.31.106:8000/sls/on_event?method=on_connect|on_close&role_name=%s&srt_url=%s&remote_ip=%s&remote_ip=%d
  in the http manager server, we can check the connection through the role name, srt_url, remote ip and remote port, if return not http reponse code 200 OK, the connection will be refused. we also can record the begin time and end time for the connection.

# 3.app
  ## app_player
  player app name, the srt url is like rtmp's, such as :srt://domain/live/stream_name ;           
  
  ## app_publisher
  the publisher app name;

  ## record_hls 
  the record hls switch, on, off, default is off.

  ## record_hls_segment_duration 
  the dutaion of ts segment, unit s, default is 10s.

# 4.relay
  ## type 
  the type of relay, support two type: pull, push;
   
  ## mode
  the relay mode, support two mode: loop, hash; 
  in the loop mode, sls will loop to connect upstreams url one by one until connection is successfully. 
  in the hash mode, sls will connect the upstreams server with the url hash.
   
  ## reconnect_interval
  reconnect interval when connection is failed, unit s;
  
  ## idle_streams_timeout
  the timeout of no data, when timeout the server will discard the relay. unit s, -1 is unlimited.  

  ## upstreams
  the relay upstream url, if there are more than one, divide with space, such as: 127.0.0.1:9090?streamid=live.sls.com/live 192.168.1.100:8080/?streamid=live.test.com/live;

