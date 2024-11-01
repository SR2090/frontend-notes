## Debouncing != Throttling

Whenever I bring up the concept of debouncing, developers try to cast it as just a means of throttling. But that’s not true at all. Throttling is the reduction in rate of a repeating event. Throttling is good for reducing mousemove events to a lesser, manageable rate, for instance.

Debouncing is quite more precise. Debouncing ensures that exactly one signal is sent for an event that may be happening several times — or even several hundreds of times over an extended period. As long as the events are occurring fast enough to happen at least once in every detection period, the signal will not be sent! 