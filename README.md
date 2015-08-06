# comkafka-php

  Comkafka.php基于https://github.com/arnaud-lb/php-rdkafka 扩展进行封装
  
  php-rdkafka基于kafka c++ library(https://github.com/edenhill/librdkafka)

  example:
  	send:
	  	$kafka = new ComKafka('kafka_host_name','topic_name','producer');
		$kafka -> produce($msg);//默认随机发送到各partition
		//$kafka -> produce($msg,$partition_id);//指定partition_id发送,需>=0且存在该partition
		//$kafka ->produce($msg,ComKafka::PRODUCER_PARTITION_MODE_CONSISTENT,$key);//使用consistenthashing算法进行发送，相同key下保序
	
	consumer:
		$kafka = new ComKafka('kafka_host_name','topic_name','consumer');
		while(true){
			$res = $kafka -> consume($partition);
			if($res){
				echo $res;
			}
		}
		
