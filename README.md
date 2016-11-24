# node-redis-mongo

Code included is based upon:
https://www.pluralsight.com/courses/play-by-play-node-web-api-john-papa-sam-artioli
https://github.com/samartioli/node-play-by-play
https://github.com/samartioli/node-web-api

To learn more about this setup, I configured the wrappers for Vagrant and Ansible.

    # run app
    cd /home/ubuntu/app
    forever stopall
    forever start cat_server.js
    forever start dog_server.js
    forever list
    nodemon pet_server.js

    # load data
    curl -X POST -s http://192.168.56.156:3000/cat -H "Content-Type: application/json" -d '{"name":"harry","age":"3","type":"siamese"}'
    curl -X POST -s http://192.168.56.156:3000/cat -H "Content-Type: application/json" -d '{"name":"sally","age":"2","type":"alley"}'
    curl -X POST -s http://192.168.56.156:3000/cat -H "Content-Type: application/json" -d '{"name":"garfield","age":"14","type":"tabby"}'
    curl -X POST -s http://192.168.56.156:3001/dog -H "Content-Type: application/json" -d '{"name":"jack","age":"9","type":"puggle"}'
    curl -X POST -s http://192.168.56.156:3001/dog -H "Content-Type: application/json" -d '{"name":"murphy","age":"9","type":"labrador"}'

    # validation
    curl -s http://192.168.56.156:3002/ping
    curl -s http://192.168.56.156:3000/cat | python -m json.tool
    curl -s http://192.168.56.156:3001/dog | python -m json.tool #5 second timeout
    time curl -s http://192.168.56.156:3002/pets | python -m json.tool

    # id specific testing
    curl -X GET -s http://192.168.56.156:3000/cat/<id> | python -m json.tool
    curl -X GET -s http://192.168.56.156:3001/dog/<id> | python -m json.tool
    curl -X PUT -s http://192.168.56.156:3000/cat/<id> -H "Content-Type: application/json" -d '{"name":"jane","age":"5","type":"persian"}'
    curl -X PUT -s http://192.168.56.156:3001/dog/<id> -H "Content-Type: application/json" -d '{"name":"sam","age":"8","type":"bulldog"}'
    curl -X DELETE http://192.168.56.156:3000/cat/<id>
    curl -X DELETE http://192.168.56.156:3001/dog/<id>

    # mongo commands
    mongo admin
    show dbs
    use cats
    show collections
    db.cats.stats()
    db.cats.find()
    db.cats.remove({})
    db.dropDatabase()

    # redis commands
    redis-cli
    keys *
    get <key>
    get http://localhost:3001/dog
    set <key> <value>
    set "http://localhost:3001/dog" "[{\"_id\":\"58324ade2c5360a72005fcb6\",\"name\":\"titus\",\"age\":2,\"type\":\"pug\",\"__v\":0}]"
    flushdb
