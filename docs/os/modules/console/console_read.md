## <font color="#F2853F" style="font-size:24pt"> console_read </font>

```no-highlight
  int
  console_read(char *str, int cnt)
```

Copies up to *cnt* bytes of received data to buffer pointed by *str*. Function tries to break the input into separate lines; once it encounters a newline character, it replaces that with end-of-string and returns.

#### Arguments

| Arguments | Description |
|-----------|-------------|
| str |  Buffer where data is copied to.  |
| cnt |  Maximum number of characters to copy.  |

#### Returned values

Returns the number of characters copied. 0 if there was no data
available, or if the first received character was '\n'.


#### Example

```no-highlight
void
task1_loop(void *arg)
{
    struct os_event *ev;
    char rx_msg[128];
    int rx_len;

    while (1) {
        ev = os_eventq_get(&task1_evq);
        assert(ev);
        if (ev->ev_type == CONS_EV_TYPE) {
            rx_len = console_read(rx_msg, sizeof(rx_msg));
            if (rx_len) {
                    if (!strncmp(rx_msg, "reset", rx_len)) {
                            assert(0);
                    }
```
