# Sbus Emulator Viewer

Maybe you already know the [Microsoft Service Bus Emulator](https://learn.microsoft.com/en-us/azure/service-bus-messaging/test-locally-with-service-bus-emulator?tabs=automated-script), thats give to you and local instance that's emulate the Azure Service Bus, enabling development tests withouth being connected on cloud.

And maybe you also know the project [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer). This one it's a wonderfull project, that gives to you a complete client to interact with Azure Service Bus.

But, when I tried to connect Service Bus Explorer with Service Bus Emulator, I discover that this not work!

So I decided to build a (very limited but functional) Service Bus Client. You can checkout the project from [blogdoft/sbus-emulator-viewer](https://github.com/blogdoft/sbus-emulator-viewer). But if you are not interested in code, you can just run this docker compose with:

```bash
docker compose up -d
```

When all containers is up, you can access [http://localhost:8080](http://localhost:8080).

## Configuring

If you just run the compose file, you do not need to configure anything.

But if you want to change the topic structure, just change `sbus-emulator/config.json` file. To more instructions about how to configure this file, [click here](https://github.com/Azure/azure-service-bus-emulator-installer/blob/main/ServiceBus-Emulator/Config/Config.json).