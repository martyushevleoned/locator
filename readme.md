# locator

## Запись дампа
Зеркалирование интерфейса
```shell
ip a
sudo iw dev wlp1s0 interface add mon0 type monitor
sudo ip link set mon0 up
sudo iw dev mon0 del
```
Запись дампа
```shell
sudo tshark -i mon0 \
    -T fields -e frame.time_epoch -e wlan.sa -e radiotap.dbm_antsignal \
    -Y "wlan.sa && radiotap.dbm_antsignal" \
    -E separator=, -E quote=d -E occurrence=f \
    | tee data/wifi.csv
```
