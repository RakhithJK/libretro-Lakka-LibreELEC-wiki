# First attempt

To keep this guide simple, we will setup two Lakka boxes in the same house, on the same local network, behind one router.

The first Lakka box, that we will call **box1** will operate as server. The other one, **box2** will operate as client.

You need to know the IP address of the server, **box1**.

On the **box1** side:

 1. Go to Settings->Network
 2. Enable Netplay
 3. Set the port to something like 3000
 4. Don't store anything in the IP field
 5. Start a two player game, for example Mario Kart on SNES

The screen will become black and stay like this until the second player connects

On the **box2** side:

 1. Go to Settings->Network
 2. Enable Netplay
 3. Enable the Client Mode
 4. Set the port to the same value you choose before
 5. In the IP field, write the IP for **box1**
 6. Start the same game

If everything is ok, the game should start on both side, you will be player#2

## Remarks

 * Netplay is based on savestates, cores not supporting savestates will not support netplay
 * The client can be in spectator mode
 * You need the exact same ROM
 * You can connect any RetroArch instances, not just Lakka ones.
