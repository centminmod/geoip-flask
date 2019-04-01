# Python Flask GeoLite2 City service

## Demo/Usage
* See information of your IP: <https://geoip.centminmod.com/>
* See information of IP 8.8.8.8: <https://geoip.centminmod.com/8.8.8.8>
* Get JSON with information of your IP: <https://geoip.centminmod.com/api/v1.0/ip/>
* Get JSON with information of IP 8.8.8.8: <https://geoip.centminmod.com/api/v1.0/ip/8.8.8.8>

## Running
Using Flask only (development):
```
python3 app.py
```

Using UWSGI:
```
/usr/local/bin/uwsgi --master --http 0.0.0.0:8888 --chdir /opt/geoip-flask/ --module app:app --processes 4
```

## Docker

```
docker run -d --net=host -p 8888:8888 --name geoip centminmod/geoip-flask
```

## Credits
* We use GeoLite2 data created by [Maxmind](http://www.maxmind.com)
