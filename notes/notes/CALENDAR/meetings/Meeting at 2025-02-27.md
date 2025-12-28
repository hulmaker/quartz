# Meeting at 2025-02-27 - tag reader
**Participants**: Erik H., Ondra, Martin, Johnny


## Meeting notes
Je potreba co nejdrive zacit reportovat zakaznikovi
Nevime jak restartovat tag reader z runtime error - muzeme killnout proces a restart service

## Follow-up tasks
- deploy pipeline to 413, run test with the tag_reader (Erik)
- najit v logu tu cast kdy jsme neco precetli a kouknout jestli lidar dal smysluplnou hodnotu. (viz minule jak vracel nesmyslne hodnoty)  (Erik)
- zaridit ze killne pipeline process na radce 108 (Johnny)
- V systemd spustit 2 joby - sensor manager z git a druhy tento script - service file z gitu a prepsat cestu do github repo (a predtim osinstalovat package) (Johnny)
- processing datagramu pred publish - deduplikace, zmena smeru vlaku (topic stejny jako train ID) \_sighting_from_tag_read (Erik)


call v 15:30
Email reporting?
pozor na train sighting id
vyplnit detection node, speed 0.0, doplnit car, car type
sensor id dostane pipeline v hlavnim configu, 401
rozsirit config co jde do PubsubPublisherComponent o sensor id


divna vzdalenost lidaru:
```
2025-02-27 08:06:57,320 [INFO] __main__: LIDAR: 2355.11[cm] at 1740643617.2034974[ts]
2025-02-27 08:06:57,326 [INFO] __main__: LIDAR in reading range, 8 > 1
2025-02-27 08:06:57,327 [DEBUG] __main__: reading tags with timeout 0.2[s]
2025-02-27 08:06:57,654 [INFO] __main__: tag: 9E3BAA94C61CC81390000000002E8739, car_id: DBUX0000340359, data: {'equipment group code': 19, 'tag type': 3, 'equipment initial': 'DBUX', 'car number': 340359, 'side indicator code': 0, 'length': 200, 'number of axles': 3, 'first check sum': 0, 'reserved frame marker': 3, 'bearing type code': 1, 'platform identifier code': 0, 'spare': 0, 'reserved': 0, 'security': 2977, 'data format code': 51, 'second check sum': 2, 'frame marker': 1}
2025-02-27 08:06:57,654 [DEBUG] __main__: sleeping for 0.2 seconds
2025-02-27 08:06:57,856 [DEBUG] __main__: waiting for lidar measurements
2025-02-27 08:06:57,857 [DEBUG] cv_pipeline.lidar.lidar_service: Getting distance measurements from interval [1740643617.6574419, 1740643617.700293]
2025-02-27 08:06:57,860 [INFO] __main__: LIDAR: 9201.00[cm] at 1740643617.6752932[ts]
2025-02-27 08:06:57,866 [INFO] __main__: LIDAR in reading range, 2 > 1
2025-02-27 08:06:57,867 [DEBUG] __main__: reading tags with timeout 0.2[s]
2025-02-27 08:06:58,214 [INFO] __main__: tag: 9E3BAA94C61CC81390000000002E8739, car_id: DBUX0000340359, data: {'equipment group code': 19, 'tag type': 3, 'equipment initial': 'DBUX', 'car number': 340359, 'side indicator code': 0, 'length': 200, 'number of axles': 3, 'first check sum': 0, 'reserved frame marker': 3, 'bearing type code': 1, 'platform identifier code': 0, 'spare': 0, 'reserved': 0, 'security': 2977, 'data format code': 51, 'second check sum': 2, 'frame marker': 1}
```

tady taky:
```
2025-02-27 08:15:08,045 [INFO] __main__: LIDAR: 236.44[cm] at 1740644107.8844666[ts]
2025-02-27 08:15:08,059 [DEBUG] __main__: reading tags with timeout 0.2[s]
2025-02-27 08:15:08,378 [INFO] __main__: tag: 9A7497CC8E4AC91790000000002E8739, car_id: GATX0000205714, data: {'equipment group code': 19, 'tag type': 1, 'equipment initial': 'GATX', 'car number': 205714, 'side indicator code': 1, 'length': 201, 'number of axles': 3, 'first check sum': 1, 'reserved frame marker': 3, 'bearing type code': 1, 'platform identifier code': 0, 'spare': 0, 'reserved': 0, 'security': 2977, 'data format code': 51, 'second check sum': 2, 'frame marker': 1}
2025-02-27 08:15:08,378 [DEBUG] __main__: sleeping for 0.2 seconds
2025-02-27 08:15:08,579 [DEBUG] __main__: waiting for lidar measurements
2025-02-27 08:15:08,580 [DEBUG] cv_pipeline.lidar.lidar_service: Getting distance measurements from interval [1740644108.3802216, 1740644108.5369644]
2025-02-27 08:15:08,582 [INFO] __main__: LIDAR: 4486.93[cm] at 1740644108.4569647[ts]
2025-02-27 08:15:08,589 [DEBUG] __main__: reading tags with timeout 0.2[s]
2025-02-27 08:15:08,948 [INFO] __main__: tag: 9A7497CC8E4AC91790000000002E8739, car_id: GATX0000205714, data: {'equipment group code': 19, 'tag type': 1, 'equipment initial': 'GATX', 'car number': 205714, 'side indicator code': 1, 'length': 201, 'number of axles': 3, 'first check sum': 1, 'reserved frame marker': 3, 'bearing type code': 1, 'platform identifier code': 0, 'spare': 0, 'reserved': 0, 'security': 2977, 'data format code': 51, 'second check sum': 2, 'frame marker': 1}
2025-02-27 08:15:08,948 [DEBUG] __main__: sleeping for 0.2 seconds
2025-02-27 08:15:09,150 [DEBUG] __main__: waiting for lidar measurements
2025-02-27 08:15:09,151 [DEBUG] cv_pipeline.lidar.lidar_service: Getting distance measurements from interval [1740644108.950986, 1740644108.9388385]
2025-02-27 08:15:09,159 [DEBUG] __main__: reading tags with timeout 0.2[s]
2025-02-27 08:15:09,461 [DEBUG] __main__: sleeping for 0.2 seconds
2025-02-27 08:15:09,663 [DEBUG] __main__: waiting for lidar measurements
2025-02-27 08:15:09,663 [DEBUG] cv_pipeline.lidar.lidar_service: Getting distance measurements from interval [1740644109.4637876, 1740644109.5416198]
2025-02-27 08:15:09,666 [INFO] __main__: LIDAR: 430.43[cm] at 1740644109.5016198[ts]
```

filter outliers, not median filter
prepsat podminku aby to bylo stejne jako to ma johnny