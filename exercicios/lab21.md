### <i class="icon-file"></i>Lab 21

Docs:
https://nodejs.org/api/events.html


#### <i class="icon-hdd"></i>  index.js

    var events = require('events');
    var eventEmitter = new events.EventEmitter();

    // listener #1
    var listner1 = function listner1() {
       console.log('listner1 executado.');
    }

    // listener #2
    var listner2 = function listner2() {
      console.log('listner2 executado.');
    }

    // Vincular o evento de conexão com a função listner1
    eventEmitter.addListener('connection', listner1);

    // Vincular o evento de conexão com a função listner2
    eventEmitter.on('connection', listner2);

    var eventListeners = require('events').EventEmitter.listenerCount
       (eventEmitter,'connection');
    console.log(eventListeners + " Listener(s) ouvindo evento de conexão");

    // Disparar o evento de conexão
    eventEmitter.emit('connection');

    // Retire a ligação da função listner1
    eventEmitter.removeListener('connection', listner1);
    console.log("Listner1 não vai ouvir agora.");

    // Disparar o evento de conexão
    eventEmitter.emit('connection');

    eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
    console.log(eventListeners + " Listener(s) ouvindo evento de conexão");

    console.log("Programa acabou.");


#### <i class="icon-hdd"></i>  package.json

    {
    "name": "lab21",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
        "start": "node index.js"
    },
    "author": "",
    "license": "ISC"
    }
  











