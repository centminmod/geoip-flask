# Python Flask GeoLite2 City service

[![](https://images.microbadger.com/badges/version/centminmod/geoip-flask.svg)](https://microbadger.com/images/centminmod/geoip-flask "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/centminmod/geoip-flask.svg)](https://microbadger.com/images/centminmod/geoip-flask "Get your own image badge on microbadger.com") [![](https://images.microbadger.com/badges/commit/centminmod/geoip-flask.svg)](https://microbadger.com/images/centminmod/geoip-flask "Get your own commit badge on microbadger.com")


## Demo/Usage
* See information of your IP: <https://geoip.centminmod.com/>
* See information of IP 8.8.8.8: <https://geoip.centminmod.com/8.8.8.8>
* Get JSON with information of your IP: <https://geoip.centminmod.com/api/v1.0/ip/>
* Get JSON with information of IP 8.8.8.8: <https://geoip.centminmod.com/api/v1.0/ip/8.8.8.8>
* Short url to get JSON with info of your IP: <https://geoip.centminmod.com/json/>
* Short url to get JSON with info of IP 8.8.8.8: <https://geoip.centminmod.com/json/8.8.8.8>

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

## Behind Centmin Mod Nginx Reverse Proxy

```
  location / {
    include /usr/local/nginx/conf/503include-only.conf;
    include /usr/local/nginx/conf/proxy.conf;
    proxy_pass http://geoip_upstream;
  }

  location ~ ^/json/(.*)$ {
    include /usr/local/nginx/conf/503include-only.conf;
    include /usr/local/nginx/conf/proxy.conf;
    proxy_pass http://geoip_upstream/api/v1.0/ip/$1;
  }
```

```
curl -s https://geoip.centminmod.com/json/8.8.8.8 | jq
{
  "continent": {
    "code": "NA",
    "geoname_id": 6255149,
    "names": {
      "de": "Nordamerika",
      "en": "North America",
      "es": "Norteamérica",
      "fr": "Amérique du Nord",
      "ja": "北アメリカ",
      "pt-BR": "América do Norte",
      "ru": "Северная Америка",
      "zh-CN": "北美洲"
    }
  },
  "country": {
    "geoname_id": 6252001,
    "iso_code": "US",
    "names": {
      "de": "USA",
      "en": "United States",
      "es": "Estados Unidos",
      "fr": "États-Unis",
      "ja": "アメリカ合衆国",
      "pt-BR": "Estados Unidos",
      "ru": "США",
      "zh-CN": "美国"
    }
  },
  "geoip_DB_MTime": "Mon Apr  1 08:43:07 2019",
  "location": {
    "accuracy_radius": 1000,
    "latitude": 37.751,
    "longitude": -97.822
  },
  "registered_country": {
    "geoname_id": 6252001,
    "iso_code": "US",
    "names": {
      "de": "USA",
      "en": "United States",
      "es": "Estados Unidos",
      "fr": "États-Unis",
      "ja": "アメリカ合衆国",
      "pt-BR": "Estados Unidos",
      "ru": "США",
      "zh-CN": "美国"
    }
  },
  "traits": {
    "ip_address": "8.8.8.8"
  }
}
```

## Credits
* We use GeoLite2 data created by [Maxmind](http://www.maxmind.com)
