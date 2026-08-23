# AI Builder Course

## 5 Tricks and 1 Trap in Agentic AI
- **Illusion of Memory (Bellek Yanılsaması):** LLM'ler doğası gereği stateless'tir (hafızaları yoktur, her isteği sıfırdan işlerler). Buradaki "hile", sisteme her seferinde geçmiş sohbet/bağlam pencerelerini ekleyerek kullanıcıya kesintisiz bir hafızası varmış illüzyonu yaşatılmasıdır.
- **Thinking / Reasoning (Düşünme / Akıl Yürütme):** Modelin sadece anlık cevap üretmek yerine; karmaşık bir görevi alt adımlara bölmesi (Chain-of-Thought), plan yapması ve "Önce ne yapmalıyım?" diye mantık süzgecinden geçirmesidir. 
    - LLM aslında bir seferde tüm metni yazmak yerine kelime kelime (token token) çalışarak otoregresif bir döngü izlerler. Model, her bir adımda inference (çıkarım) yaparak mevcut bağlam üzerinden bir sonraki olasılığı hesaplar ve ilk token'ı üretir. Ardından ürettiği bu yeni veriyi hemen girdinin (input) sonuna ekler; yenilenen bu büyük bağlamı tekrar işleyerek bir sonraki çıkarım adımıyla sonraki token'ı tahmin eder. Cümle sonunu belirten özel bir durdurma simgesi (stop token) gelene kadar bu çıkarım süreci milisaniyeler içinde binlerce kez tekrarlanır. Dolayısıyla modelin metin üretirken her defasında anlık çıkarımlarla chunk chunk, yani adım adım girdiyi zenginleştirerek ilerlemesi onun temel çalışma mekanizmasını oluşturur.
    - Ayrıca bu modeller mimari olarak "Chat" ve "Reasoning" varyantları şeklinde karşımıza çıkar; ancak bazı durumlarda Chat varyantları Agentic AI uygulamalarında çok daha iyi performans gösterebilir. Öte yandan, gelişmiş modeller üzerinde çalışırken sistemin ne kadar derinlikli düşüneceğini ayarlamak için "reasoning effort" (akıl yürütme çabası) veya "thinking budget" (düşünme bütçesi) parametrelerini belirleyerek sürecin performansını ve maliyetini optimize edebilirsiniz.
    - Bu süreçte yapay zeka, milyonlarca bağlantı için önceden eğitilmiş sayısal katsayılar olan ağırlıkları (weights) kullanır; hangi kelimeye, kurala veya mantık adımına değer vereceğini ise bilinçli bir kararla değil, o anki bağlama göre matematiksel olasılıklarla tamamen kendi seçer.
- **Chaining LLMs (LLM Zincirleme):** Tek bir modelin her şeyi kusursuz yapamayacağı durumlarda, birden fazla modelin veya prompt adımının birbirine bağlanmasıdır (Örn: Bir modelin çıkışı, diğerinin girdisi olur; biri metin yazar, diğeri kodu kontrol eder).
- **Tools (Araçlar):** Yapay zekanın sadece kendi içindeki veriyle sınırlı kalmayıp; web araması yapması, veritabanına bağlanması (örneğin PostgreSQL), API'leri tetiklemesi (Marketstack vb.) veya kod çalıştırması gibi dış dünyayla etkileşime geçmesini sağlayan yetenekleridir.
- **The Loop (Döngü):** Ajanın doğrusal (tek yönlü) çalışmak yerine; bir görevi yapıp sonucu değerlendirmesi, hata alırsa (örneğin senin yaşadığın Marketstack tarih hatası gibi) hatayı görüp parametreleri değiştirerek hedefe ulaşana kadar süreci kendi kendine tekrarlamasıdır (ReAct döngüsü).
- **The Human Trap (İnsan Tuzağı):** Sistemin her şeyi tamamen otonom yapabileceğine güvenip insan denetimini (Human-in-the-loop) tamamen ortadan kaldırmaktır. Ajanlar halüsinasyon görebilir, sonsuz döngüye girebilir veya yanlış bir aracı tetikleyip sistemi bozabilir. En büyük tuzak, yapay zekayı tamamen başıboş bırakmaktır; kritik kararlarda insanın onay vermesi her zaman emniyet supaplı olmalıdır.

## N8N Terminology
- **Node:** A single step in a business process can be a Trigger or an Action
- **Connection:** A link - passes data from the output of one node to the input of another
- **Workflow:** A collection of nodes connected together to automate a process
- **Execution:** A single run of a workflow; can be Manual (testing) or Active (production)
- **Templates:** A prebuilt workflow that you can use as a starting point
- **Cloud:** A hosted environment where workflows run securely on cloud infrastructure without requiring local server management
- **Instance:** An isolated, running environment or deployment of an application (such as an n8n installation) containing its own workflows, data, and settings

[First Integration](./workflows/first%20integration.json): It integrates Google Sheets and Marketstack as AI tools to retrieve, manage, and update portfolio data based on financial queries.

[Second Integration](./workflows/second%20integratio.json): It integrates Gmail tools to retrieve recent messages (filtered by the last 5 days) and send automated emails to tuncaydataengineer@gmail.com.