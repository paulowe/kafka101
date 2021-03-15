# Apache Kafka 101
 
 ## What is Apache Kafka?
 Apache Kafka is a distributed streaming platform. It simplifies data ingestion and consumption from multiple sources to multiple target systems.
 
 ## About this repo
Here you will find companion code and exercises from the Apache Kafka for beginners course I completed by Stephane Maarek's udemy class. I include my notes and architecture screenshots.

## Development environment set-up (MacOS)
1. Make sure you have [Apache Kafka](https://kafka.apache.org/downloads)  binary downloaded
2. Add Kafka to your PATH by editing your .bash_profile or .zsh_profile. `export PATH='$PATH:/path/to/kafka_2.x.x/bin'`
3. For this application, make sure you have Java8 installed on your system
   - Check Java version `java -version`. If not Java8 and OS == MacOS:
   - `brew tap homebrew/cask-versions`
   - `brew cask install java8`
