                   _       _                _
     ___  ___ _ __(_) __ _| | ___  ___  ___| |
    / __|/ _ \ '__| |/ _` | |/ _ \/ __|/ __| |
    \__ \  __/ |  | | (_| | | (_) \__ \ (__|_|
    |___/\___|_|  |_|\__,_|_|\___/|___/\___(_)

     serialosc is an osc server for yr monome

     it is a daemon that waits for you to
     plug a monome in, then it spawns off a
     dedicated server process to route OSC
     messages to and from your monome.  it
     also advertises a _monome-osc._udp
     service over zeroconf (bonjour).

                               wrl@illest.net



# Development

## Building

Install [libmonome](https://github.com/monome/libmonome)

* macOS `brew install libmonome`
* Some other stuff for Linuxes
* Windows? Dunno.

Compile serialosc

```
./waf configure
./waf
```

## Running

```
./build/bin/serialoscd
```

To install to a system wide location

`./waf install`

## Extending

Adding new OSC functions to serialosc is easy!

Add callback functions in `serialosc-device/server.c` to handle messages from your device with the following signature

```
void handle_press(const monome_event_t *e, void *data)
```

Register the function with the following interface defined in `libmonome/public/monome.h`

```
int monome_register_handler(monome_t *monome, monome_event_type_t event_type,
                            monome_event_callback_t, void *user_data);
```

## Device Discovery

Registering a device to serialosc works like this?

While extending functionality of a device is easy, registering a new device is hard.

