# Tuya switch WB2S (rf-module)
<p>
Configure tuya switch OpenBK7231T
</p>
<img src="https://github.com/Alexxx113/Tuya-switch-WB2S-rf-module-/blob/main/IMG_20220716_181325%20(1).jpg" alt="альтернативный текст" />

<p></p>
<p>remove mcu</p>
<p>solder wire</p>
<img src="https://github.com/Alexxx113/Tuya-switch-WB2S-rf-module-/blob/main/solder.jpg" alt="альтернативный текст" />



<p></p>
<b>Flashing for <red>BK7231T</red></b>
<p></p>
<p>Go to pages firmware instruction</p>


<a href="https://github.com/openshwprojects/OpenBK7231T_App">OpenBK7231T_App</a>

<p></p>
<p>connect uart 3.3v !!!!</p>


<p></p>
<p>conect new WIFI "openbk..."</p>
<p>go "192.168.4.1"</p>
<p>configure WIFI</p>
<p></p>
<b>configure module:</b>
<p></p>
<p>P7 btn 1</p>
<p>P8 rel 1</p>


<p>configure MQTT</p>

<b>home assistant config:</b>
<p>"name" = name switch</p>

<div class="snippet-clipboard-content notranslate position-relative overflow-auto" data-snippet-clipboard-copy-content="">
  <pre class="notranslate">
  <code>
light:
  - platform: mqtt
    unique_id: "name"
    name: "name"
    state_topic: ""name"/1/get"
    command_topic: ""name"/1/set"
    qos: 1
    payload_on: 1
    payload_off: 0
    retain: true
    availability_topic: ""name"/connected"
  </code>
  </pre>
</div>

<b>if you want add temp sensor:</b>
<p>P23 adc 2</p>
<p>NTC thermistor a B value of 3950 100k</p>
<p>resistor 20k</p>

<img src="https://github.com/Alexxx113/Tuya-switch-WB2S-rf-module-/blob/main/IMG_20220716_181325.jpg" alt="альтернативный текст" />
<img src="https://github.com/Alexxx113/Tuya-switch-WB2S-rf-module-/blob/main/temp.jpg" alt="альтернативный текст" />

<b>home assistant config:</b>
<p>"name" = name switch</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto" data-snippet-clipboard-copy-content="">
  <pre class="notranslate">
  <code>  
sensor:
  - platform: mqtt
    state_topic: ""name"/2/get"
    name: "mqtt temp sens"
    qos: 1
    device_class: power
    availability_topic: ""name"/connected"
  </code>
  </pre>
</div
  <p>"name" = name switch</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto" data-snippet-clipboard-copy-content="">
  <pre class="notranslate">
  <code>
template:
  sensor:
     - name: Temperatura NTC kabinet
      unique_id: temperature_kabinet
      device_class: temperature 
      state: >
        {% set Vo = states('sensor.mqtt_temp_sens')|float %}
        {% set res = 200000 %}
        {% set term  = 100000 %}
        {% set nom_t  = 27 %}
        {% set adc  = 3584 %}
        {% set B = 3950 %}

        {% set tr  =  res / ((adc / Vo) - 1)  %}
        {% set steinhart = term /  tr%}
        {% set steinhart1 = log(steinhart) %}
        {% set steinhart2 = steinhart1 / B %}
        {% set steinhart3 = steinhart2 + (1.0 / (nom_t + 273.15))%}
        {% set steinhart4 = 1.0 / steinhart3  %}
        {% set steinhart5 = steinhart4 - 273.15%}

        {{ steinhart5  |round(2) }}
      unit_of_measurement: '°C'
  </code>
  </pre>
</div>
