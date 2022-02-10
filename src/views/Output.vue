<template>
    <h1>Code Generated!!</h1>
    <h4 style = "padding:10px;">
        Upload the code below to your Arduino Board. Testing the code on Wokwi Simulator first is always a great idea!
    </h4>
<div class="links">
  <w-button @click = "copyToClipboard" class = "ma1" bg-color = "info" lg>Copy to Clipboard</w-button>

  <a href="https://wokwi.com/arduino/projects/323111706679050836" target = "_blank">
  <w-button class="ma1" bg-color = "success" style = "padding:5px; font-size:14;" lg>Simulate on Wokwi</w-button>
  </a>

  <w-notification
    v-model="showNotification"
    :timeout="timeout"
    sucess
    plain
    round
    shadow>
    Copied to Clipboard!
  </w-notification>

</div>
<br/>
<v-ace-editor
    v-model:value="content"
    @init="editorInit"
    lang = 'c_cpp'
    :printMargin = "false"
    theme="monokai"
    wrap
    style="height: 300px; width: 60%; align-self: center;" />


<Footer/>


</template>




<script>

import { VAceEditor } from 'vue3-ace-editor';
import 'ace-builds/src-noconflict/theme-monokai';
import 'ace-builds/src-noconflict/mode-c_cpp';
import Footer from '@/components/Footer.vue'
export default {
    name: 'Output',
    props: {
        events: Array
    },
    components: {
        VAceEditor,
        Footer,
    },
    methods: {
        editorInit(){},
        copyToClipboard(){
          navigator.clipboard.writeText(this.content);
          this.showNotification = !this.showNotification;
        }
    },
    data() {
        return {
            Events: [],
            content: "",
            timeout: 2000,
            showNotification: false
        }
    },
    mounted(){
        let data = this.$route.params.events;
        if(data != undefined){
            let count = 0;
            while(count < data.length){
            this.Events.push(JSON.parse(data[count]));
            count++;
            }
            // Adding code to Editor
            var today = new Date();
            let content1 = "/*\n\
 * --------------------------------------------------------------------------------------\n\
 * Team FreshBOTS submittion to BUILDABOT Contest.\n\
 * \n\
 * This is a project to build a Events Manager/Reminder Bot using Arduino\n\
 * Features include alarms for classes, reminders to stay hydrated, take a walk/break\n\
 * Every 15 mins it goes through all the upcoming events so youre refreshed every moment\n\
 * and structure your day on the fly.\n\
 * \n\
 * Read Full Documentation here:\n\
 * Github Repository: https://github.com/mostlyaman/botaminder-code-generator/\n\
 * ---------------------------------------------------------------------------------------\n\
 * \n\
 * ==============================================================================\n\
 *   CREDITS for Tune Playing Program\n\
 *   Original Melody from All Star, by Smash Mouth\n\
 *   Inspiration from https://workshops.hackclub.com/coffin_dance_arduino/\n\
 *   Music code from bansalrohan18\n\
 *   https://www.tinkercad.com/things/fMHcz0D6nag\n\
 * ==============================================================================\n\
 *\n\
 *\n\
 *\/\n\
// ==============================================================================\n\
// ==============================================================================\n\
\n\
// TOKEN HERE PLEASE\n\
\n\
long time[3] = { " + today.getHours().toString() + " , " + today.getMinutes().toString() + " , " + today.getSeconds().toString() + " };\n\
int events = " + this.Events.length.toString() + ";\n\
String eventName[" + this.Events.length.toString() + "] = { ";
            count = 0;
            while(count<this.Events.length){
                content1 += "\""+this.Events[count].name+"\"";
                if(count !== this.Events.length - 1){
                    content1 += ", ";
                }
                count++;
            }
            content1+= " };\n\
long eventStartTime["+ this.Events.length.toString() + "] = { ";

            count=0;
            while(count<this.Events.length){
                content1+= "(long)"+this.Events[count].startHour.toString()+"*3600+(long)"+this.Events[count].startMin.toString()+"*60";
                if(count !== this.Events.length-1){
                    content1+= ", ";
                }
                count++;
            }
            content1+= " };\n\
long eventEndTime[" + this.Events.length + "] = { ";

            count=0;
            while(count<this.Events.length){
                content1+="(long)"+this.Events[count].endHour.toString()+"*3600+(long)"+this.Events[count].endMin.toString()+"*60";
                if(count!== this.Events.length-1){
                  content1+=", "
                }
                count++;
            }
            content1+=" };\n\
int eventScrollingSpeed = 4;\n\
long waterReminder = (long)3*3600;\n\
long breakReminder = (long)4*3600;\n\
long eveningBreak = (long)17*3600;\n\
\n\
String userMode = \"manual\";\n\
\n\
\n\
// TOKEN ENDS HERE\n\
// =============================================================================\n\
// =============================================================================\n\
\n\
#include <LiquidCrystal.h>\n\
\n\
#define pushButton 3\n\
#define mutePin 2\n\
\n\
String getShortTime(long eventTime);\n\
long getLongTime();\n\
void updateTimeBySeconds(int x);\n\
void printTime();\n\
void updateTime();\n\
void muteDevice();\n\
void buttonFunction();\n\
void play(float hz, int wait);\n\
void alarm();\n\
int currentSpeaker = 4;\n\
int currentEvent = 0;\n\
long timeWhileAlarmOn1;\n\
bool recordingTimeAlarmOn1 = false;\n\
long timeWhileAlarmOn2;\n\
bool recordingTimeAlarmOn2 = false;\n\
int eventScrollingSpeedCounter = 0;\n\
bool notHourZero = true;\n\
bool notMinZero = true;\n\
bool notSecZero = true;\n\
String mode = userMode;\n\
int passedEvents = 0;\n\
int breakPassedEvents = 1;\n\
int waterPassedEvents = 1;\n\
long timeForSetup;\n\
bool alarmOn1 = false;\n\
bool alarmOn2 = false;\n\
bool alarmHealthEvents = true; \n\
bool alarmNormalEvents = true;\n\
long waterBreak[8];\n\
long breakBreak[6];\n\
int currentHealthEvent = 0;\n\
LiquidCrystal lcd(9,8,13,12,11,10);\n\
LiquidCrystal lcd2(9,7,13,12,11,10);\n\
\n\
void setup() {\n\
  timeForSetup = millis();\n\
  lcd.begin(16,2);\n\
  lcd.begin(16,2);\n\
\n\
\n\
\n\
  pinMode(pushButton, INPUT);\n\
  pinMode(mutePin, INPUT);\n\
  pinMode(4, OUTPUT);\n\
  pinMode(5, OUTPUT);\n\
  // set up the LCD's number of columns and rows:\n\
  lcd.begin(16, 2);\n\
  lcd2.begin(16,2);\n\
\n\
  long cur_time = getLongTime();\n\
  int var = 0;\n\
  while(cur_time + var*waterReminder < 86399){\n\
    waterBreak[var] = cur_time + var*waterReminder;\n\
    var++;\n\
  }\n\
\n\
  var = 0;\n\
  while(cur_time + var*breakReminder < 86399){\n\
    breakBreak[var] = cur_time + var*breakReminder;\n\
    var++;\n\
  }\n\
\n\
  if(mode == \"events\"){alarmHealthEvents = false;}\n\
  else if(mode == \"health\"){alarmNormalEvents = false;}\n\
  else if(mode == \"silent\"){alarmHealthEvents = false; alarmNormalEvents = false;}\n\
  \n\
  if(digitalRead(mutePin) == LOW){mode = \"muted\\n\";}\n\
  attachInterrupt(digitalPinToInterrupt(mutePin), muteDevice, CHANGE);\n\
  attachInterrupt(digitalPinToInterrupt(pushButton), buttonFunction, FALLING);\n\
\n\
  updateTimeBySeconds((millis()-timeForSetup)/1000);\n\
}\n\
\n\
void loop() {\n\
  long currentTime = getLongTime();\n\
  if(alarmNormalEvents && !alarmOn2){\n\
    if(!digitalRead(mutePin) && !recordingTimeAlarmOn1 && alarmOn1){\n\
      recordingTimeAlarmOn1 = true;\n\
      timeWhileAlarmOn1 = millis();\n\
    }\n\
    if(currentTime == eventStartTime[passedEvents] && !alarmOn1){\n\
      timeForSetup = millis();\n\
      alarmOn1 = true;\n\
      lcd.clear(); lcd2.clear();\n\
      lcd.print(\"ALARM\"); lcd.setCursor(0,1); lcd.print(\"Hurry UP !!!\");\n\
      lcd2.print(eventName[passedEvents]); lcd2.setCursor(0,1);\n\
      lcd2.print(getShortTime(eventStartTime[passedEvents])); lcd2.print(\" - \"); lcd2.print(getShortTime(eventEndTime[passedEvents]));\n\
    }\n\
\n\
    if(alarmOn1 && digitalRead(mutePin)){alarm();}\n\
  }\n\
  if(alarmHealthEvents && !alarmOn1){\n\
    if(!digitalRead(mutePin) && !recordingTimeAlarmOn2 && alarmOn2){\n\
      recordingTimeAlarmOn2 = true;\n\
      timeWhileAlarmOn2 = millis();\n\
    }\n\
    if(!alarmOn2 && currentTime == waterBreak[waterPassedEvents]){\n\
      timeForSetup = millis();\n\
      alarmOn2 = true;\n\
      currentHealthEvent = 0;\n\
      lcd.clear(); lcd2.clear();\n\
      lcd.print(\"Water Reminder\"); lcd.setCursor(0,1); lcd.print(\"Stay Hydrated!\");\n\
      lcd2.print(\"Last Drink At\"); lcd2.setCursor(0,1);\n\
      lcd2.print(getShortTime(waterBreak[waterPassedEvents-1]));\n\
    }\n\
    if(!alarmOn2 && currentTime == breakBreak[breakPassedEvents]){\n\
      timeForSetup = millis();\n\
      alarmOn2 = true;\n\
      currentHealthEvent = 1;\n\
      lcd.clear(); lcd2.clear();\n\
      lcd.print(\"Break Reminder\"); lcd.setCursor(0,1); lcd.print(\"Rest your eyes!\");\n\
      lcd2.print(\"Last Break At\"); lcd2.setCursor(0,1);\n\
      lcd2.print(getShortTime(breakBreak[breakPassedEvents-1]));\n\
    }\n\
    if(!alarmOn2 && currentTime == eveningBreak){\n\
      timeForSetup = millis();\n\
      alarmOn2 = true;\n\
      currentHealthEvent = 2;\n\
      lcd.clear(); lcd2.clear();\n\
      lcd.print(\"Evening Break\"); lcd.setCursor(0,1); lcd.print(\"Go for a walk?\");\n\
      lcd2.print(\"Some exercise?\"); lcd2.setCursor(0,1); lcd2.print(\"Some coffee?\");\n\
    }\n\
    if(alarmOn2 && digitalRead(mutePin)){alarm();}\n\
  }\n\
  if(!alarmOn1 && !alarmOn2){\n\
  \n\
  timeForSetup = millis();\n\
  lcd.clear(); lcd2.clear();\n\
  lcd.setCursor(0,0); lcd.print(\"mode: \");lcd.print(mode); printTime();\n\
  lcd2.setCursor(0,0); lcd2.print(eventName[currentEvent]); lcd2.setCursor(0,1); \n\
  lcd2.print(getShortTime(eventStartTime[currentEvent])); lcd2.print(\" - \"); lcd2.print(getShortTime(eventEndTime[currentEvent]));\n\
  eventScrollingSpeedCounter++;\n\
  \n\
  if(eventScrollingSpeedCounter == eventScrollingSpeed){\n\
    currentEvent++; eventScrollingSpeedCounter = 0;\n\
    if(currentEvent == events){currentEvent = 0 + passedEvents;}\n\
    }\n\
    \n\
  updateTime();\n\
  delay(975-(millis()-timeForSetup)/1000);\n\
  }\n\
}\n\
\n\
long getLongTime(){\n\
  return time[0]*3600 + time[1]*60 + time[2];\n\
}\n\
  \n\
String getShortTime(long eventTime){\n\
  String s1 = String(eventTime/3600);\n\
  if(s1.length() == 1){s1 = \"0\"+s1;}\n\
  String s2 = String((eventTime%3600)/60);\n\
  if(s2.length() == 1){s2 = \"0\"+s2;}\n\
  return s1 + \":\" + s2;\n\
}\n\
\n\
void updateTimeBySeconds(int x){\n\
  long temp = getLongTime() + x;\n\
  time[0] = temp / 3600;\n\
  time[1] = (temp%3600)/60;\n\
  time[2] = temp%60;\n\
}\n\
\n\
void printTime(){\n\
  lcd.setCursor(0,1);\n\
  lcd.print(\"Time: \");\n\
  for(int i = 0; i<3; i++){\n\
    if(time[i]<10){lcd.print(0);}\n\
    lcd.print(time[i]);\n\
    if(i != 2){lcd.print(\":\");}\n\
  }\n\
}\n\
\n\
void updateTime(){ \n\
  if(time[2]>58){\n\
    if(time[1]>58){\n\
      if(time[0]>22){\n\
        time[0] = 0;\n\
        notHourZero = false;\n\
      }\n\
      if(notHourZero){time[0]++;}\n\
      notHourZero = true;\n\
      time[1] = 0;\n\
      notMinZero = false;\n\
    }\n\
    if(notMinZero){time[1]++;}\n\
    notMinZero = true;\n\
    time[2] = 0;\n\
    notSecZero = false;\n\
  }\n\
  if(notSecZero){time[2]++;}\n\
  notSecZero = true;\n\
}\n\
\n\
void muteDevice(){\n\
  if(digitalRead(mutePin) == LOW){\n\
    mode = \"muted  \";}\n\
  else if(digitalRead(mutePin) == HIGH){\n\
    mode = userMode;}\n\
}\n\
  \n\
void buttonFunction(){\n\
  if(alarmOn1){\n\
    alarmOn1 = false;\n\
    if(!(passedEvents+1 == events)){\n\
    passedEvents++;}\n\
    lcd.clear(); lcd2.clear();\n\
    lcd.print(\"Alarm Muted!\"); lcd.setCursor(0,1);\n\
    lcd.print(\"Next Alarm -->\");\n\
    lcd2.print(eventName[passedEvents]); lcd2.setCursor(0,1);\n\
    lcd2.print(getShortTime(eventStartTime[passedEvents])); lcd2.print(\" : \"); lcd2.print(getShortTime(eventEndTime[passedEvents]));\n\
    if(recordingTimeAlarmOn1){updateTimeBySeconds((millis()-timeWhileAlarmOn1)/1000); recordingTimeAlarmOn1 = false;}\n\
  }\n\
  else if(alarmOn2){\n\
    alarmOn2 = false;\n\
    if(currentHealthEvent == 0){waterPassedEvents++;}\n\
    else if(currentHealthEvent == 1){breakPassedEvents++;}\n\
    lcd.clear(); lcd2.clear();\n\
    lcd.print(\"Alarm Muted!\"); lcd.setCursor(0,1);\n\
    if(recordingTimeAlarmOn2){updateTimeBySeconds((millis()-timeWhileAlarmOn2)/1000); recordingTimeAlarmOn2 = false;}\n\
  }\n\
}\n\
\n\
/*\n\
 * Credits for Tune Playing Code\n\
 * Original Melody from All Star, by Smash Mouth\n\
 * Inspiration from https://workshops.hackclub.com/coffin_dance_arduino/\n\
 * Music code from bansalrohan18\n\
 * https://www.tinkercad.com/things/fMHcz0D6nag\n\
 *\/\n\
void play(float hz, int wait) {\n\
\n\
  tone(currentSpeaker, hz, 1000);\n\
  delay(200);\n\
  noTone(currentSpeaker);\n\
  delay(wait);\n\
  \n\
  if(currentSpeaker == 4) {\n\
    currentSpeaker += 1;\n\
  } else {\n\
      currentSpeaker -= 1;\n\
  }\n\
}\n\
\n\
void alarm() {\n\
  int alarmTime = millis();\n\
  float hertz[] = {392, 587.33, 493.88, 493.88, 440, 392, 392, 523.25, 493.88, 493.88, 440, 440, 392, 392, 523.25, 493.88, 493.88, 440, 440, 392, 440, 329.63};\n\
  float wait[] = {200, 70, 100, 300, 100, 200, 130, 200, 70, 70, 70, 70, 200, 70, 70, 70, 70, 70, 70, 70, 70, 1000};\n\
  for(int i = 0; i < 22; i++){\n\
    if(alarmOn1 || alarmOn2){play(hertz[i], wait[i]);}\n\
  }\n\
  updateTimeBySeconds((millis()-alarmTime)/1000);\n\
\n\
}\n\
";
            this.content = content1;
        }else{
            this.$router.push({name: "Home"});
            alert("Inputs not clear. Plese Try Again! This usually happens if the output page is reloaded.");
        }
    },

}
</script>

