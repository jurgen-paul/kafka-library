# kafka-library 
git@github.com:jurgen-paul/kafka-library.git

echo "# kafka-library" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:jurgen-paul/kafka-library.git
git push -u origin main

git remote add origin git@github.com:jurgen-paul/kafka-library.git
git branch -M main
git push -u origin main 
const { Kafka } = require('@confluentinc/kafka-javascript').KafkaJS;

async function producerStart() {
    const producer = new Kafka().producer({
        'bootstrap.servers': '<fill>',
        'security.protocol': 'SASL_SSL',
        'sasl.mechanisms': 'PLAIN',
        'sasl.username': '<fill>',
        'sasl.password': '<fill>',
    });

    await producer.connect();
    console.log("Connected successfully");

    const res = []
    for (let i = 0; i < 50; i++) {
        res.push(producer.send({
            topic: 'test-topic',
            messages: [
                { value: 'v', partition: 0, key: 'x' },
            ]
        }));
    }
    await Promise.all(res);

    await producer.disconnect();
    console.log("Disconnected successfully");
}

producerStart();

node -e 'console.log(require("@confluentinc/kafka-javascript").librdkafkaVersion)'
