# 10 Minutes Panic Scaling - Chat with Admin KKS-TNI AD 2020

![](.\img\info.png)

Panic ~~Attack~~ Scaling adalah langkah yang dilakukan problem setter / penulis pada kompetisi KKS-TNI AD 2020. Pada problem / soal **Chat With Admin**. Sekilas **Chat With Admin** adalah sebuah problem di mana melakukan **SQL Injection** pada Robot / BOT **Whatsapp** yang telah disediakan.  Garis besar soal **Chat With Admin** adalah adanya simple filter yang mana tidak dapat melakukan payload SQLi sederhana dan tidak ada error yang dikeluarkan oleh responnya. Dan lagi untuk mendapatkan nomor **Whatsapp** dari Robot/BOT ini harus melakukan dan menyelesaikan soal OSINT terlebih dahulu.



Permasalahan hadir saat soal **Chat With Admin** sudah rilis sekitar kurang lebih 10 menit. Tiba-tiba tidak ada respon dari BOT Whatsapp-nya. Sebelumnya seperti inilah skema yang bekerja pada soal **Chat With Admin**.



![](.\img\d1.png)

Pada dasarnya secara sederhana seorang player/hacker yang mengirimkan chat akan diterima oleh sistem bot lalu bot akan melakukan http requests ke Rest API yang berada pada sebuah Domain yang shared hosting. Tujuanya kenapa menggunakan konsep Rest API sebenarnya selain mudah untuk dikembangkan juga untuk mempermudah proses SQL injectionnya. 



## Permasalahan

Permasalahan kenapa bisa down? Jawabanya karena saya melakukan deploy Rest API di sebuah Shared Hosting dan kesalahan utamanya bukan karena saya deploy di shared hosting, tapi bagaimana saya mengimplementasikan Rest API tersebut. Saya mengirimkan requests http dari BOT wa ke Rest API menggunakan methode **GET** inilah dugaan terkuat saya kenapa bisa down, bukan down juga tapi Shared Hosting melakukan **Blocking** terhadap **IP BOT Whatsapp-**nya karena dianggap sebagai Malicious Requests berupa SQLi, namun hal ini blocking ini baru saya sadari beberapa hari setelah KKS-T selesai sebenarnya, waktu perlombaan saya tetap yakin shared hosting saya down karena ratusan requests secara cepat.



# Panic Solving

Di waktu perlombaan, saya sendiri tidak begitu banyak memiliki solusi untuk ini. Karena saya di awal memiliki **Hipotesa** bahwa Shared Hostingnya down terkena ratusan requests. Jadi yang saya pikirkan adalah dengan cepat melakukan Scaling atau men-deploy ke banyak server lalu melakukan Load Balancing. Jadi seperti inilah konsep yang saya gunakan saat perlombaan. Di tulisan kali ini saya tidak membahas secara teknis hanya bentuk cerita dan memberikan gambaran saja bagaimana konsepnya.

![](.\img\d2.png)

Sekarang pada konsep yang baru dengan menggunakan Load Balancing, saya melakukan deploy ke 2 server saja sebenarnya, keduanya adalah server pribadi saya dan yang menjadi Load Balancing Nginx-nya adalah saya meminjam Server tempat saya bekerja. Dan sampai perlombaan selesai tidak ada issue down atau tidak bisa diakses, semuanya berjalan dengan sangat lancar!



# Kesimpulan

Panic Scaling ini hanya dilakukan dalam kurun waktu 10 menit saja, menurut saya sangat cepat sekali karena memang sebelumnya saya sudah menyiapkan worst scenario untuk soal ini.  Dan docker-docker di tiap server juga sudah tinggal deploy. Jadi solusinya sebenarnya tidak perlu melakukan ini / Load Balancing, seharunya mungkin bisa requestsnya dibuat POST agar lebih smooth(?). Tapi memang saya juga belum tau cara yang lebih efektif dalam situasi seperti ini. Terima kasih telah membaca!