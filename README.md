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


