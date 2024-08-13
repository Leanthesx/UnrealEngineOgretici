# Unreal Engine Ögretici
![uebanner](https://github.com/user-attachments/assets/79e931c4-2655-4a45-9baa-bb75a2552d20)

Selamlar, bu eğitim serisinde sizlere Unreal Engine hakkında bildiklerimi aktaracağım.

### İÇİNDEKİLER
[1.IDE Nedir?](#1IDE-Nedir)

[2.Temel Sınıflar ve Kavramlar](#2Temel-Sınıflar-ve-Kavramlar)

[2.1.ReflectionSystem](#21ReflectionSystem)

[2.2.UnrealHeaderTool](#22UnrealHeaderTool)

[2.3.CoreMinimal.h](#23CoreMinimal.hl)

[2.4.Engine.h](#24Engine.h)

## 1.IDE Nedir?
IDE(Integrated Development Environment) türkçesiyle Tümleşik Geliştirme Ortamı, bir yazılımcının programlama dilini yazdığı uygulamadır. IDE, yazılım geliştirmek için gerekli tüm araçları birleştiren bir yazılım paketidir. Kod editörü, hata ayıklama özelliği, derleyici ve otomatik kod tamamlama gibi özellikler içerir. Size biri ücretsiz biri ücretli iki tane IDE önerisinde bulunacağım.

![vstudio](https://github.com/user-attachments/assets/8c8bbd6a-7d18-4e13-b5db-b8cd00ef786b)

Bunlardan birincisi, hepimizin bildiği Microsoft Visual Studio. Windowsun sitesinde yazan özellikleri:
- İş yükü tabanlı yükleyici - Yalnızca ihtiyacınız olanı yükleyin
- Güçlü kodlama araçları ve özellikleri - Uygulamalarınızı tek bir yerde oluşturmak için ihtiyacınız olan her şey
- Birden çok dil desteği - C++, C#, JavaScript, TypeScript, Python ve daha birçok dilde kod
- Platformlar arası geliştirme - Herhangi bir platform için uygulama derleme
- Sürüm denetimi tümleştirmesi - Ekip arkadaşlarıyla kod üzerinde işbirliği yapma
- Yapay zeka destekli geliştirme - Yapay zeka yardımıyla kodu daha verimli yazma

Türkçe dil desteği ve ücretsiz sürümünün olması da sizin için bir artı olabilir.

![rideride](https://github.com/user-attachments/assets/a0357465-5b13-483d-a363-91e1770ee9ae)

İkincisi ise Rider. Rider, Unreal Engine için biçilmiş kaftandır. C++ syntax desteğinin daha geniş olması, performansının daha iyi olması onu Visual Studionun önüne geçiriyor. Eksiklerinden bir tanesi Ram kullanımının fazla olması. Eğer bu IDE'yi kullanacaksanız RAM belleğinizin yeterli olacağından emin olun. Maalesef ki Visual Studio gibi Community sürümüne sahip değil. Bu yüzden 30 günlük deneme sürümünün ardından aylık ödeme sistemine geçiyor. Benim tercihim kesinlikle Riderdir. Ama Visual Studio da geri kalmış bir IDE değil aksine günümüzün en güçlü IDE'leri arasındadır.

İki IDE'nin karşılaştırmasını [şu](https://www.jetbrains.com/rider/compare/rider-vs-visual-studio/) linkten inceleyebilirsiniz.

## 2.Temel Sınıflar ve Kavramlar
Unreal Engine'de C++ projesi oluşturduğumuzda birkaç tane Header File(Başlık Dosyası) oluşmaktadır. Bu .h uzantılı dosyalar, gerekli olan Unreal Engine sınıflarını, veri türlerini ve işlevlerini içerir. Bunlara göz atmadan önce UnrealHeaderTool'un ve Reflection System'in ne olduğunu öğrenelim.

### 2.1.ReflectionSystem
Reflection System'in ne olduğunu açıklamadan önce Metadata Specifier'ini öğrenelim. Metadata; UClasses, UFunctions, UProperties, UEnums ve UInterfaces tanımlarken Unreal Engine editöründe nasıl davranacaklarını belirlemek için kullanılır. Meta verilerini Unreal Header Tool(UHT) üretir. Metadata Specifier'i tanımlamak için "meta" anahtar kelimesi kullanılır ve her veri yapısı veya üyesinin kendine ait Metadata Specifier listesi vardır. 

![enummetadataspecifier](https://github.com/user-attachments/assets/933bdd35-4970-40cb-a905-49755b7b41e9)

Yukarıdaki fotoğrafta, Enumerated türünde kullanılabilecek Metadata Specifier'lerini görüyoruz.

Reflection System, Metadata ve tür bilgilerini runtime sırasında erişilebilir hale getiren bir sistemdir. Bu sistem, Unreal Engine'in kendi C++ sınıflarını ve veri yapısını anlamasına, düzenlemesine ve üzerinde işlem yapmasına olanak tanır. Reflection System ile aşağıdaki işlemler yapılabilir:

- UCLASS, UPROPERTY, UFUNCTION gibi makrolar kullanılarak sınıfların, özelliklerin ve fonksiyonların Unreal Engine'e özgü özellikleri belirlenir.
- Türler arası dönüştürme işlemleri, tür bilgisi üzerinde çalışma ve dinamik nesne oluşturma işlemleri yapılabilir.
- C++ sınıflarının Blueprintler içinde kullanılmasını sağlar. Örneğin, UPROPERTY makrosu, belirli bir C++ değişkeninin Blueprint içinde editlenebilir hale gelmesini sağlar.
- Verilerin kaydedilip yüklenmesi işlemleri için önemlidir.

### 2.2.UnrealHeaderTool
Unreal Header Tool (UHT), Unreal Engine için kod oluşturma aracıdır. UHT, kaynak dosyalarını tarar ve "UCLASS", "USTRUCT", "UENUM", "UPROPERTY", "UFUNCTION" gibi makroları arar. Bu makroların bulunduğu yerlerde, UHT gerekli meta verileri üretir. Bu meta veriler, daha sonra "Generated.h" dosyalarına yerleştirilir ve Reflection System tarafından kullanılır. 
Unreal Engine C++ projesinde, kodların derlenmesi 2 aşama ile gerçekleşir.

- Unreal Build Tool(UBT) UHT'yi çağırır ve yukarıdaki işlemler yapılır.
- UBT, sonucu derlemesi için C++ Compiler'ini çağırır.


### 2.3.CoreMinimal.h
CoreMinimal.h dosyası, genellikle daha büyük başlık dosyalarının sağladığı ek işlevsellik ve bağımlılıklardan kaçınarak, yalnızca en temel ve sık kullanılan özellikleri sunar. Sadece en gerekli bileşenleri içine dahil ettiği için derleme süresi ve performansı optimize etme açısından önemli bir role sahiptir. İçeriği:
- Nesnelerin pozisyonlarını, yönelimlerini ve dönüşlerini ayarlamak için kullanılan "FVector", "FRotator", "FTransform"
- Veri yapıları ve veri yönetimini sağlamak için kullanılan "TArray", "TMap", "TSet"
- Metinsel ifadeleri düzenlemek için kullanılan "FString", "FText", "FName"
- Yansıma sistemi ve sınıf yapısını tanımlamak için kullanılan makrolar "UCLASS", "USTRUCT", "UENUM", "UPROPERTY", "UFUNCTION" ve diğer temel özellikler bu header dosyasının içinde bulunmaktadır.

Herhangi bir C++ dosyası açtığımızda(None, Character, Actor, ActorComponent, SceneComponent, Interface, GameModeBase vb.) CoreMinimal.h dosyası eklenmiş bir şekilde gelir.

### 2.4.Engine.h
Engine.h dosyası, motorun tüm özelliklerine erişim sağlar ve derleme süresi uzundur. İçerdiği bileşenlere ek olarak fizik motoru, ağ özellikleri, animasyon sistemleri, yapay zeka ve diğer yüksek seviye Unreal Engine modüllerini de içerir. İçeriği: 
- Temel motor bileşenleri olan "UObject", "AActor", "GameMode", "GameState", "PlayerController"
- Görselleştirme ve grafik işlemleri için kullanılan "UPrimitiveComponent", "UMeshComponent", "UStaticMesh", "USkeletalMesh", "UMaterial", "UCameraComponent", "ACameraActor", "Post-Processing"
- Fizik işlemleri için kullanılan "UPhysicsConstraintComponent", "UPhysicalMaterial", "ULandscapeComponent", "ULandscapeLayerInfoObject"
- Ses sistemi için kullanılan "USoundBase", "USoundCue", "UAudioComponent"
- Animasyon sistemi için kullanılan "USkeletalMeshComponent", "UAnimSequence", "UAnimInstance"
- Yapay zeka ve navigasyon işlemleri için kullanılan "AAIController", "UBehaviorTree", "UAIPerceptionComponent", "UNavigationSystem", "UNavMeshBoundsVolume", "UPathFollowingComponent"
- Input işlemleri için kullanılan "UInputComponent", "UPlayerInput", "UGameViewportClient"
- Replication ve ağ için kullanılan "UNetDriver", "UReplicationGraph", "UActorChannel"
- Kayıt ve oyun durumu için kullanılan "USaveGame", "UGameplayStatics" ve daha fazlası bu header dosyasının içinde bulunmaktadır.

Bu iki modül arasındaki en önemli fark optimizasyon ve derleme süresidir. CoreMinimal.h dosyası en temel ve sık kullanılan modülleri içerdiği için derleme süresi kısadır; fakat Engine.h daha geniş bir işlevsellik sunar, bu yüzden derleme süresi uzundur ve performans açısından daha zorlayıcıdır. 
