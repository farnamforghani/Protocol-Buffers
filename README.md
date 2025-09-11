# Protocol-Buffers

نگارندگان: فرنام فرقانی، آرین ایروانی، کیان تراکمه


# بیان مسئله

در عصر نرم‌افزارهای مدرن، تبادل داده بین سیستم‌ها و سرویس‌ها به یک نیاز حیاتی تبدیل شده است. این داده‌ها باید ساختار مشخصی داشته باشند و مستقل از زبان برنامه‌نویسی یا پلتفرم، توسط طرف مقابل قابل استفاده باشند.  

## چالش‌های قالب‌های متنی متداول

روش‌های متداولی مانند **JSON** و **XML** اگرچه ساده و خوانا هستند، اما محدودیت‌هایی دارند که در مقیاس بزرگ نمود پیدا می‌کند:

- **حجم داده نسبتاً زیاد**: کلیدها و برچسب‌های تکراری باعث افزایش حجم فایل و ترافیک شبکه می‌شوند.
- **پردازش کندتر**: عملیات تجزیه و ساختاردهی داده متنی در مقایسه با قالب‌های دودویی زمان بیشتری می‌طلبد.
- **انعطاف‌پذیری محدود در تغییر ساختار**: کوچک‌ترین تغییر در قالب داده می‌تواند ناسازگاری بین نسخه‌های مختلف ایجاد کند.
- **مصرف بالاتر منابع**: در سناریوهای با پهنای باند محدود، ارسال و دریافت داده متنی بهینه نیست.

## اهمیت موضوع در معماری‌های بزرگ

در سیستم‌های توزیع‌شده (Distributed Systems)، سرویس‌های مایکروسرویس (Microservices) و ارتباطات بین‌زبانی (Cross-Language Communication)، این محدودیت‌ها می‌تواند منجر به مشکلات جدی مانند کاهش عملکرد، افزایش هزینه زیرساخت، و پیچیدگی مدیریت داده شود.

## نیاز به راهکاری بهینه و سازگار

برای رفع این چالش‌ها، نیاز به یک راهکار سریع‌تر، کم‌حجم‌تر، و با قابلیت سازگاری نسخه‌ای (Backward/Forward Compatibility) احساس شد.  
**Protocol Buffers** که توسط گوگل توسعه یافته است، دقیقاً با هدف حل این مشکلات طراحی شده و با استفاده از ساختارهای داده دودویی و تعریف شِما به زبان مستقل، امکان تبادل داده بهینه را بین سیستم‌های ناهمگون فراهم می‌کند.

![img.png](assets/protobuf.png)

# معرفی کلی

## مقدمه

**Protocol Buffers** (به اختصار **Protobuf**) یک قالب سریال‌سازی داده ساختارمند و مستقل از زبان است که توسط گوگل توسعه یافته است. این فناوری ابتدا در سال ۲۰۰۱ ایجاد شد و در سال ۲۰۰۸ به‌صورت متن‌باز منتشر گردید.  
Protobuf با هدف تبادل کارآمد داده بین سیستم‌های مختلف طراحی شده و داده‌ها را به‌صورت دودویی (Binary) ذخیره و منتقل می‌کند که این امر باعث کاهش حجم و افزایش سرعت پردازش می‌شود.

## مفهوم اساسی و فرآیند کار
در Protobuf، ساختار داده‌ها ابتدا با استفاده از یک زبان توصیفی ساده در قالب فایل‌های شِما با پسوند **`.proto`** تعریف می‌شود.  
این فایل‌ها انواع داده و فیلدها را به همراه شماره برچسب (Tag Number) مشخص می‌کنند که نقش مهمی در فشردگی داده و سرعت پردازش دارد.

سپس این شِما توسط کامپایلر مخصوص Protobuf (مانند `protoc`) به کد قابل استفاده در زبان‌های مختلف (C++، Java، Python، Go و بیش از ۲۰ زبان دیگر) تبدیل می‌شود. این فرآیند، کلاس‌ها و توابع لازم برای عملیات سریال‌سازی (Encoding) و دسریال‌سازی (Decoding) را به‌صورت خودکار ایجاد می‌کند.

![img.png](assets/protobuf-workflow.png)

## مزایای کلیدی

### ۱. کارایی بالا در حجم و سرعت
- داده‌ها در قالب دودویی فشرده ذخیره می‌شوند که حجم آن را تا حدود ۱۰ برابر کمتر از JSON و سرعت پردازش را تا ۶ برابر سریع‌تر از XML می‌کند.
- این بهینه‌سازی باعث کاهش پهنای باند مصرفی و بهبود عملکرد سیستم می‌شود.

### ۲. سازگاری نسخه‌ای (Backward/Forward Compatibility)
- امکان تغییر ساختار داده بدون شکستن سازگاری با نسخه‌های قدیمی یا جدید.
- مناسب برای توسعه تدریجی بدون ایجاد اختلال در سرویس‌های موجود.

### ۳. استقلال از زبان و پلتفرم
- Protobuf مستقل از زبان برنامه‌نویسی و پلتفرم است.
- مناسب برای معماری‌های چند‌پایانه (Multi-platform) و سیستم‌های توزیع‌شده.

### ۴. تعریف دقیق و رسمی ساختار داده
- فایل‌های `.proto` به‌عنوان منبع واحد تعریف داده، وضوح و قابلیت نگهداری بالاتری را برای پروژه‌ها فراهم می‌کنند.

## کاربردهای اصلی
- سرویس‌های وب و APIها (از جمله **gRPC**).
- سیستم‌های مایکروسرویسی و ارتباطات بین سرویس‌ها.
- اپلیکیشن‌های موبایل و سرویس‌های ابری.
- سیستم‌های پیام‌رسانی (Message Queuing).
- ذخیره‌سازی داده در پایگاه داده یا فایل.

Protobuf امروزه به‌عنوان یک استاندارد کارآمد و قابل اعتماد برای تبادل داده در مقیاس بزرگ شناخته می‌شود و شرکت‌هایی مانند گوگل، Netflix و Uber از آن در مقیاس وسیع استفاده می‌کنند.

# مثال

در این بخش، نحوه استفاده از Protocol Buffers را با یک مثال عملی از سیستم مدیریت کاربران نشان می‌دهیم.

## تعریف شِما (.proto)

ابتدا ساختار داده‌های خود را در فایل `user.proto` تعریف می‌کنیم:

```protobuf
syntax = "proto3";

package com.example;

option java_package = "com.example.protobuf";
option java_outer_classname = "UserProtos";

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
  repeated string phone_numbers = 4;
  Address address = 5;
  UserType type = 6;
}

message Address {
  string street = 1;
  string city = 2;
  string country = 3;
  int32 postal_code = 4;
}

enum UserType {
  REGULAR = 0;
  PREMIUM = 1;
  ADMIN = 2;
}
```

## کامپایل کردن شِما

برای تولید کد Java از دستور زیر استفاده می‌کنیم:

```bash
protoc --java_out=./src/main/java user.proto
```

این دستور کلاس‌های `UserProtos.java` را در مسیر مشخص‌شده ایجاد می‌کند.

## پیاده‌سازی در Java

### ۱. ساخت و پر کردن شیء

```java
import com.example.protobuf.UserProtos.*;

public class ProtobufExample {
    public static void main(String[] args) {
        // initialize Address
        Address address = Address.newBuilder()
            .setStreet("خیابان امیرآباد")
            .setCity("تهران")
            .setCountry("ایران")
            .setPostalCode(1234567890)
            .build();
        
        // initialize User
        User user = User.newBuilder()
            .setId(12345)
            .setName("رضا شکلات")
            .setEmail("reza.shokolat@example.com")
            .addPhoneNumbers("09123456789")
            .addPhoneNumbers("02112345678")
            .setAddress(address)
            .setType(UserType.PREMIUM)
            .build();
        
        System.out.println("User created: " + user.getName());
    }
}
```

### ۲. سریال‌سازی (Serialization)

```java
// array to byte
byte[] serializedData = user.toByteArray();
System.out.println("User serialized to byte array, size: " + serializedData.length + " bytes");

// saving to file
try (FileOutputStream output = new FileOutputStream("user.pb")) {
    user.writeTo(output);
    System.out.println("User serialized to file user.pb");
} catch (IOException e) {
    e.printStackTrace();
}
```

### ۳. دسریال‌سازی (Deserialization)

```java
// reconstruct from byte array
try {
    User deserializedUser = User.parseFrom(serializedData);
    System.out.println("Deserialized User Name: " + deserializedUser.getName());
} catch (InvalidProtocolBufferException e) {
    e.printStackTrace();
}

// reading from file
try (FileInputStream input = new FileInputStream("user.pb")) {
    User fileUser = User.parseFrom(input);
    System.out.println("User read from file: " + fileUser.getName());
    for (String phone : fileUser.getPhoneNumbersList()) {
        System.out.println("- " + phone);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

## مقایسه با JSON

برای نشان دادن مزیت Protocol Buffers، همان داده را با JSON مقایسه می‌کنیم:

### JSON معادل:
```json
{
  "id": 12345,
  "name": "رضا شکلات",
  "email": "reza.shokolat@example.com",
  "phone_numbers": ["09123456789", "02112345678"],
  "address": {
    "street": "خیابان امیرآباد",
    "city": "تهران", 
    "country": "ایران",
    "postal_code": 1234567890
  },
  "type": "PREMIUM"
}
```

### نتایج مقایسه:
- **حجم JSON**: حدود ۳۵۰-۴۰۰ بایت
- **حجم Protobuf**: حدود ۱۲۰-۱۴۰ بایت  
- **کاهش حجم**: تقریباً ۶۰-۷۰% کمتر
- **سرعت پردازش**: تقریباً ۳-۵ برابر سریع‌تر

## نکات مهم

### سازگاری نسخه‌ای
اگر بخواهیم فیلد جدیدی اضافه کنیم:

```protobuf
message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
  repeated string phone_numbers = 4;
  Address address = 5;
  UserType type = 6;
  string salam = 7; // new field
}
```

کد قدیمی همچنان کار می‌کند و فیلد جدید را نادیده می‌گیرد.
این قابلیت باعث می‌شود که بتوانیم به‌راحتی ساختار داده را بدون نگرانی از ناسازگاری تغییر دهیم.
### مدیریت فایل‌های وابستگی

برای پروژه‌های Maven، وابستگی زیر را اضافه کنید:

```xml
<dependency>
    <groupId>com.google.protobuf</groupId>
    <artifactId>protobuf-java</artifactId>
    <version>3.24.0</version>
</dependency>
```

این مثال نشان می‌دهد که چگونه Protocol Buffers می‌تواند راهکاری قدرتمند و کارآمد برای تبادل داده بین سیستم‌های مختلف باشد.


# مراجع

* [Google Developers — *Protocol Buffers Overview*](https://developers.google.com/protocol-buffers/docs/overview)
* [Google Developers — *Encoding*](https://developers.google.com/protocol-buffers/docs/encoding)
* [Wikipedia — *Protocol Buffers*](https://en.wikipedia.org/wiki/Protocol_Buffers)
* [Baeldung — *Introduction to Google Protocol Buffers*](https://www.baeldung.com/google-protocol-buffers)