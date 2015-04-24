var net = require('net');


var clients = [];

var server = net.createServer(function (socket) {
    
    socket.name = socket.remoteAddress;
        
    clients.push(socket);    

    //console.log(client);

    socket.on('data', function(data) {
        broadcast(data, socket);
    });
    
    socket.on('end', function() {
        clients.splice(clients.indexOf(socket), 1);
        process.stdout.write("SOMEONE HAS LEFT\n");
        broadcastLeave(socket.name); 
    });
   

});

server.listen(4000, '0.0.0.0');

function broadcast( msg, sender) {
    clients.forEach(function(client) {
        if(client != sender)
            client.write(sender.name+": "+msg);
    });   

};

function broadcastLeave(socket) {
    clients.forEach(function(client) {
        client.write(socket +" has left");    
    });
};
