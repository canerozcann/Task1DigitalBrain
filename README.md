Herkese merhaba, bu kısımda sizlere Task’ımızın ilk bölümü olan  

• install kafka using docker. 

• create a kafka topic using kafka cli command. 

• send message to kafka topic using kafka cli command. 

• listen messages produced on some topic using kafka cli command. 

  

Başlıklarını nasıl tamamladığımı anlatacağım. 

Task’ımıza başlamak için ilk olarak “• install kafka using docker.” için https://www.docker.com/ üzerinden cihazıma uygun olan güncel Docker Versionunu indirdim.  

 

Yükleme tamamlandıktan sonra Kafka'yı Docker kullanarak kurmak ve Kafka CLI komutlarını kullanarak temel işlemleri gerçekleştirmek için aşağıda bahsedeceğim aşamalara geçtim. 

 

Docker kullanarak Kafka ve Zookeeper'ı çalıştırmak için Docker Compose dosyasını oluşturmanız gerekecek bunun için Visual Studio üzerinden aşşağıda belirttiğim kodu yazdım ve bu kodu docker-compose.yml dosyasını oluşturarak içeriğini yazdım.  

 

version: '3.1' 

  

services: 

  zookeeper: 

    image: wurstmeister/zookeeper 

    container_name: zookeeper 

    ports: 

      - "2181:2181" 

  kafka: 

    image: wurstmeister/kafka 

    container_name: kafka 

    ports: 

      - "9092:9092" 

    environment: 

      KAFKA_ADVERTISED_HOST_NAME: localhost 

      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181 

 

Öncelikli olarak masaüstüme kafka-installation adında bir dosya oluşturdum ve bu dosyayı visual studio üzerinden açıp içine docker-compose.yml adında dosyamı oluşturarak içerisine üstte belirttiğim kodumu ekledim. Bu aşamalardan sonra terminal üzerinde “ cd Desktop/kafka-installation “ konumuna giderek “ docker-compose up –d  kodu “ ile birlikte Docker Compose’u çalıştırdım. Bunların ardından terminalde aynı konum üzerindeyken (kafka-installation) Docker konteynerine bağlanmak için “ docker exec -it <kafka_container_id> /bin/bash “ kodunu kullanmam gerekti.  

Bu kod üzerinde bulunan “ <kafka _container_id> “ yi öğrenmek için terminale  “ docker ps –a “ komutunu yazdığımda terminal bana  bağlanmam gereken container ID sini göstermiş oluyor. ID yi öğrenip “ docker exec -it 4c5987a96d40 /bin/bash “ ile birlikte docker container’a bağlandım. 

 

Ardından “ kafka-topics.sh --create --topic digital-brain-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1 ”  

 

Kodu ile birlikte  kendime digital-brain-topic adında bir topic oluşturdum 

 

Şimdi ise bu topic e mesaj göndermem gerekliydi bunu ise “ kafka-console-producer.sh --topic digital-brain-topic --bootstrap-server localhost:9092 “ 

 

Kodu ile birlikte açmış olduğum topic’in içine  “ Hello I’m “caner  “ mesajını gönderdim. 

 

Task’ımızın son aşamasında ise gönderdiğim bu mesajı dinlemek var. Bunu ise şu kodu kullanarak yaptım “  kafka-console-consumer.sh --topic digital-brain-topic --bootstrap-server localhost:9092 --from-beginning “  

 

Terminal üzerinde bu kodu çalıştırdığımda ise ilgili topic üzerindeki mesajım terminal ekranına gelmiş oldu ve mesajımı dinlemiş oldum 

 
<img width="574" alt="1" src="https://github.com/user-attachments/assets/33a576bf-7ca9-4dfc-b9dc-0c8ecb4138d9">

 <img width="574" alt="2" src="https://github.com/user-attachments/assets/babe4112-93ea-4afb-8e20-114270dbfeee">

<img width="574" alt="3" src="https://github.com/user-attachments/assets/914af02c-f346-418e-bbe3-5a391fc9951d">

 
