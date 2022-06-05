# LM-35--LE-SICAKLIK
ARDUİNO İLE SICAKLIK UYGULAMASI
# Arduino ve LabVIEW ile LM35 Uygulaması

 Bu uygulamada LM35 sensöründen alınan veriler LabVIEW' aktarılmıştır.

## Proje Dosyası Hakkında

Arduino kodlarını içermektedir. Serial portla haberleşme sağlanıp Arduino Nano' nun A0 bacağına bağlanan pinden analog okuma yapılır. 

 

## LM35  Dosyası Hakkında

Projenin VI dosyasını içerir. Front panelde Gauge gösterge paneli, 3 tane gösterge ledi, 2 tane numerik kontrol paneli,1 tane port kontrol paneli ,  1 tane numeric indicator ve1tane, stop durdurma düğmesi bulunmaktadır. Back panelde VISA haberleşmesi yapılıp döngü içinde daha önceden belirlenen  değerlere göre karşılaştırma yapılmaktadır.



## Images Hakkında

Projenin farklı durumlardaki fotoğrafını içerir.

## Nasıl Çalışır

 Yazdığımız Arduino kodlarını Arduino'ya yüklüyoruz. Serial olarak Arduino ile haberleşme sağlayıp oluşturduğumuz LabVIEW dosyasını açıyoruz. Açılan projede serial port panelinden Arduino'yu bağladığımız COM'u seçmeli ve referans değerlerini belirlemeliyiz.

Arduino'nun A0 pinine bağlı olan LM35 sensöründen okunan değerler VI'daki Gauge  göstergesinden okunabilir . Belirlenen referans değerlerine göre ışık şiddetini ledlerle görebiliriz.

## NOT
LabVIEW projesini çalıştırmadan önce Serial portta Arduinonun bağlı olduğu COM seçilmeli ve ışık şiddeti referans değerleri yazmamız gerekir.


## Arduino Kodları

int lm35Pin = A0;
int led = 8;

int zaman = 50;
int okunan_deger = 0;
float sicaklik_gerilim = 0;
float sicaklik = 0;
void setup()
{
pinMode(led,OUTPUT);

Serial.begin(9600);
}
void loop()
{
okunan_deger = analogRead(lm35Pin);
sicaklik_gerilim = (okunan_deger / 1023.0)*5000;
sicaklik = sicaklik_gerilim /10.0;
Serial.println(sicaklik);
if(sicaklik >= 30){
digitalWrite(led,HIGH);

delay(zaman);
digitalWrite(led,LOW);

delay(zaman);
}
else{
digitalWrite(led,LOW);

}
}
