# Disruptor Forewarning
An application monitoring tool that processes an application's event stream looking for tends that need attention.  Common use cases include variance in business event counts, application exceptions or performance degradation.

## Design
Disruptor Forewarning is based off of the disruptor pattern, a high performance inter-thread messaging library.  As events are received they are processed by any number of configured monitors.  Each monitor is backed by an in memory ring buffer.  This buffer stores the events it is interested in while another process continuously interogates the events looking for specific conditions.  The buffer is sized based on desired precision and frequency of events and can be quickly resized if needed.

### Speed
The design affords incredable speed.  All state information is stored in memeory.  No databases, no syncronous diskwrites, How is this possible?  Because each buffer entry is reused as events enter and exit scope there is little to no need for garbage collection meaning the heap can be very large.  Large heaps are associated with long JVM pauses while garbage collection occurs but if there is no garbage there are no pauses.   
