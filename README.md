# comkafka-php

  Comkafka.php基于https://github.com/arnaud-lb/php-rdkafka 扩展进行封装
  
  php-rdkafka基于kafka c++ library(https://github.com/edenhill/librdkafka)

  example:
 
    public function actionProduce(){

        $topic_name = 'jinglin_test2';//如果该topic不存在，则会创建一个partition为0的topic

        $kafka = new ComKafka($topic_name,'producer','kafka_local');
        for ($i=0; $i < 10000; $i++) { 
            $msg = 'message:'.$i;
            $kafka -> produce($msg);
        }
        //$kafka -> produce($msg);//默认，一次链接中随机发送到各partition
        //$kafka -> produce($msg,$partition_id);//指定partition_id(int)发送,需>=0且存在该partition
        //$kafka -> produce($msg,ComKafka::PRODUCER_PARTITION_MODE_CONSISTENT,$key);//使用consistent hashing算法进行发送，相同key下保序


    }
    public function actionConsumer(){

        $topic_name = 'jinglin_test2';

        $kafka = new ComKafka($topic_name,'consumer','kafka_local');
        while(true){
            $res = $kafka -> consume();
            if($res){
                echo $res."\n";
            }
        }
        // $res = $kafka -> consume();//若不指定partition，则消费全部
        // $res = $kafka -> consume(0);//指定partition_id(int)，多进程情况下使用
        // $res = $kafka -> consume(array(0,1,2));//指定多partition
    }
        

  @todo monitor class