# Rule Sets RU

Этот репозиторий содержит автоматически обновляемые наборы правил (Rule Sets) для различных инструментов маршрутизации трафика (Sing-box, V2Ray и др.).

## 📥 Файлы

- 🌍 **GeoIP**
  - _v2ray.dat_: https://github.com/aligotr/rule-set-ru/releases/latest/download/geoip.dat
  - _Mihomo.mrs_
    - 🔁 https://github.com/aligotr/rule-set-ru/releases/latest/download/geoip_proxy.mrs
  - _Sing-box.srs_
    - 🔁 https://github.com/aligotr/rule-set-ru/releases/latest/download/geoip_proxy.srs
- 🔗 **GeoSite**
  - _v2ray.dat_: https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite.dat
  - _Mihomo.mrs_
    - ➡️ https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_direct.mrs
    - 🔁 https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_proxy.mrs
    - 🚫 https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_block.mrs
  - _Sing-box.srs_
    - ➡️ https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_direct.srs
    - 🔁 https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_proxy.srs
    - 🚫 https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_block.srs

## 📁Состав

**GeoIP**
  - geoip.dat    - private, ru-blocked (antifilter-ipsum, discord-voice-ips)
  - geoip_proxy  - antifilter-ipsum, discord-voice-ips

**GeoSite**
  - geosite.dat     - private, category-gov-ru, category-ads-all, win-spy, ru-blocked (antifilter-community, re-filter), youtube, discord
  - geosite_direct  - private, category-gov-ru
  - geosite_block   - win-spy, category-ads-all
  - geosite_proxy   - ru-blocked (antifilter-community, re-filter), youtube, discord

## 📦 Как использовать

Актуальные версии правил доступны в разделе [**Releases**](../../releases). Вы можете напрямую ссылаться на URL файлов в ваших конфигурациях приложений для их автоматического обновления.

### Пример для Mihomo

#### Маршрутизация через списки

```yaml
rule-providers:
  apps-direct:
    type: http
    behavior: classical
    format: yaml
    url: https://github.com/aligotr/rule-set-ru/releases/latest/download/apps_windows_direct_mihomo.yaml
    path: ./rules/apps_windows_direct_mihomo.yaml
    interval: 86400

  geosite-proxy:
    type: http
    behavior: domain
    format: mrs
    url: https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite_proxy.mrs
    path: ./rules/geosite_proxy.mrs
    interval: 86400

rules:
  - RULE-SET,apps-direct,DIRECT
  - RULE-SET,geosite-proxy,→ Remnawave
  - MATCH,DIRECT
```

#### Маршрутизация через замену основных файлов

```yaml
geodata-mode: true
geox-url:
  geoip: https://github.com/aligotr/rule-set-ru/releases/latest/download/geoip.dat
  geosite: https://github.com/aligotr/rule-set-ru/releases/latest/download/geosite.dat

rules:
  - GEOIP,PRIVATE,DIRECT
  - GEOSITE,CATEGORY-ADS-ALL,REJECT
  - GEOIP,RU-BLOCKED→ Remnawave
  - GEOSITE,RU-BLOCKED,→ Remnawave
  - MATCH,DIRECT
```

### Пример для Sing-box

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "geoip",
        "type": "remote",
        "format": "binary",
        "url": "https://github.com/aligotr/rule-set-ru/releases/latest/download/geoip_proxy.srs",
        "download_detour": "proxy"
      }
    ]
  }
}
```

---

_Посмотреть состав dat-файлов: https://jomertix.github.io/geofileviewer/_

_Сборка основана на инструментах [Loyalsoldier](https://github.com/Loyalsoldier) и других open-source проектах._
