# collectd-python-php-fpm-status

PHP-FPM status monitor for collectd

## INSTALLATION

1.  Place `phpfpm.py` in your CollectD python plugins directory, for example `/usr/local/lib/collectd/python/`
2.  Configure the plugin in CollectD (see below)
3.  Restart CollectD

## COLLECTD CONFIGURATION

Edit your `/etc/collectd/collectd.conf` file, it should look like this:

    LoadPlugin python
    <Plugin python>
        ModulePath "/usr/local/lib/collectd/python"
        Import "phpfpm"
        <Module phpfpm>
                Url "http://127.0.0.2/pool_1_status?json&full"
        </Module>
        <Module phpfpm>
                Url "http://127.0.0.2/pool_2_status?json&full"
        </Module>
        <Module phpfpm>
                Url "http://127.0.0.2/pool_N_status?json&full"
        </Module>
    </Plugin>

You can add as many Module instances as you whish, each one pointing to a different server url.
Don't forget to add the `?json&full` query params, they are essential for this plugin to work.

## DATA FORMAT

The data is collected using the format:

`phpfpm.pool-gauge-metric` for the master process, and
`phpfpm.pool-process-N.gauge-metric` for each child process

## Enjoy!
