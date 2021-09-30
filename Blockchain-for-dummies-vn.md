# Blockchain & Bitcoin cho phó thường dân

![Bitcoin](assets/title-vn.jpg)

*[Image by MichaelWuensch from Pixabay](https://pixabay.com/users/michaelwuensch-4163668/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2007769)*

Nhà bác học Einstein từng nói: *"Nếu anh không thể giải thích vấn đề một cách đơn giản, nghĩa là anh chưa thực sự hiểu nó"*.

Blockchain là một khái niệm không còn mới với dân công nghệ, nhưng với hầu hết mọi người, nó vẫn rất mới và đặc biệt khó hiểu.

Như một nỗ lực trong việc tự đánh giá lại khả năng hiểu biết của bản thân trong quá trình nghiên cứu về blockchain và các ứng dụng của nó, tôi sẽ cố gắng viết lại theo cách *dễ hiểu nhất* có thể, những gì mình thu lượm được về lĩnh vực này. Các bài viết sẽ được đăng thành nhiều phần, song hành với quá trình nghiên cứu của tôi, như một dạng kết quả được đúc rút lại, trong những comment bên trong post này.

Các thông tin tham khảo phần lớn sẽ đến từ đồng tiền số đầu tiên ứng dụng blockchain: [Bitcoin](https://bitcoin.org). 

## Phần 1: Blockchain là gì?

Một *blockchain* là một chuỗi (*chain*) kết nối các khối (*block*) dữ liệu với nhau theo nguyên tắc: block sau phải chứa *chuỗi hash* của block trước nó, và cứ như thế cho đến tận block đầu tiên (block zero).

Vậy chuỗi hash là gì? Người ta nghĩ ra một thuật toán, gọi là *thuật toán băm* (*hash algorithm*), mà khi đưa vào đó một khối dữ liệu bất kỳ, sẽ cho ra kết quả là một chuỗi ký tự có độ dài cố định, ngắn hơn rất nhiều so với khối dữ liệu đầu vào, được gọi là *hash digest*, hay đơn giản là *hash*. Và quan trọng nhất, đó là chỉ cần một thay đổi nhỏ nhất ở dữ liệu đầu vào, thì hash đầu ra sẽ thay đổi hoàn toàn. Không thể có 2 khối dữ liệu đầu vào khác nhau, dù chỉ 1 bit, mà lại sinh ra 2 hash giống nhau. Vì thế, hash có vai trò như một chữ ký đại diện cho dữ liệu đầu vào.

Phần tiếp theo sẽ giải thích vì sao blockchain yêu cầu mỗi block phải chứa hash của block trước nó.

## Phần 2: Vì sao một block cần chứa hash của block trước nó?

Là để đảm bảo tính toàn vẹn (*integrity*) về dữ liệu của toàn bộ blockchain.

Khi ta nhận được một blockchain, ta nên kiểm tra xem liệu dữ liệu của nó có bị sai lệch hay không. Trong thực tế có rất nhiều khả năng dẫn đến sai lệch dữ liệu: lỗi đường truyền, lỗi ổ cứng, dính virus, bị cố tình sửa đổi...

Vậy làm thế nào để kiểm tra sự toàn vẹn của blockchain? Rất đơn giản: giả sử blockchain có độ dài N blocks, ta sẽ lấy dữ liệu của block N-1 đưa vào thuật toán hash để tạo ra chuỗi hash của nó, rồi so sánh với giá trị chuỗi hash đang được lưu trữ ở block N. Nếu bằng nhau, nghĩa là blockchain đang OK với 2 block N và N-1. Tiếp tục làm như vậy cho đến block zero. Nếu mọi phép so sánh đều cho kết quả bằng nhau, ta sẽ yên tâm rằng dữ liệu của blockchain này là toàn vẹn. Nếu chỉ cần xuất hiện một kết quả khác nhau, ta sẽ kết luận ngay blockchain này không còn toàn vẹn.

Tuy nhiên thiết kế này chỉ đưa ra cách kiểm tra tính toàn vẹn của blockchain, chứ chưa đảm bảo *tính đúng đắn* (*validity*) của nó. Đây là nội dung của phần tiếp theo.

## Phần 3: Tính đúng đắn của blockchain

*Đây là một chủ đề dài, và sẽ cần nhiều phần.*

Một blockchain toàn vẹn không có nghĩa là nó đúng đắn. Một kẻ rành công nghệ có thể tạo ra một blockchain toàn vẹn về dữ liệu, nhưng trong đó chứa đựng những dữ liệu sai khác với thực tế và có lợi cho hắn. Việc này rất dễ dàng: giả sử blockchain hiện có độ dài là 5, gồm các block A-B-C-D-E. Bill, là một kẻ xấu xa, cần sửa đổi dữ liệu ở block C, hắn ta sẽ làm việc đó, rồi tính toán lại hash của block C, đưa hash này vào block D, tiếp tục tính hash của block D, đưa vào block E. Và thế là xong. Hắn đã tạo ra một blockchain toàn vẹn về dữ liệu, nhưng chứa dữ liệu lừa đảo có mục đích, rồi tung ra cho mọi người cùng xem. Như thế, giờ đây tồn tại 2 blockchain, và chúng chỉ giống nhau từ block B về trước, còn từ block C thì khác nhau. Vậy làm thế nào để biết blockchain nào là đúng đắn (valid)?

Có một cách rất dễ dàng: chúng ta bầu ra một người, có tên là Peter, đứng ra xác định blockchain nào là đúng đắn. Peter là một anh chàng đàng hoàng, có uy tín, có tiếng là trung thực, vì thế đa số đều tin vào anh ta. Thế nhưng, nhỡ đâu Peter lại mắc sai sót? Hoặc thậm chí, anh ta thông đồng với Bill, và xác nhận blockchain của Bill là đúng?

Tốt nhất là không dựa vào một cá nhân nào, vì ở thời buổi này, chẳng ai đáng tin cả. Nhưng nếu thế, thì làm thế nào xác nhận tính đúng đắn của một blockchain? Đây là thách thức lớn mang tính quyết định với những người tìm cách ứng dụng blockchain. Giải pháp cho thách thức này được trình bày ở phần tiếp theo.

## Phần 4: Cơ chế đồng thuận

Để xác định một sự việc nào đó đúng hay sai, cơ chế truyền thống sử dụng những cá nhân hoặc tổ chức được bầu chọn hoặc chỉ định, mà ví dụ dễ hiểu nhất là một ông quan tòa. Nhưng đi kèm theo đó là các nguy cơ hiển nhiên: ông quan tòa có năng lực yếu kém, mắc sai sót khi xét xử, bị mua chuộc... và đưa ra phán quyết không công bằng.

Để khắc phục, người ta bổ sung vào đó bồi thẩm đoàn, là những người dân thường được lựa chọn ngẫu nhiên, để theo dõi và đưa ra nhận định về phiên tòa. Quan tòa bắt buộc, theo luật, phải tuân theo kết luận của bồi thẩm đoàn. Thế nhưng, thực tế đầy rẫy ví dụ về việc thành viên bồi thẩm đoàn bị mua chuộc, hoặc mắc sai lầm do định kiến. Có gì lạ đâu, bồi thẩm đoàn chỉ cỡ 10 hay 12 vị mà thôi. Do đó về bản chất, đây vẫn là cơ chế *đồng thuận tập trung* (*centralized consensus*), chứa đựng đầy rẫy những nguy cơ đưa ra các quyết định không công bằng. Những kẻ xấu: quan tham, trùm mafia, giới chủ độc ác... không thiếu tiền cùng các biện pháp để tấn công, mua chuộc từ bồi thẩm đoàn đến quan tòa.

Tốt nhất, là đưa ra một cơ chế *đồng thuận phi tập trung* (*decentralized consensus*), trong đó số lượng thành viên là không dự đoán được (unpredictable), danh tính các thành viên ban bồi thẩm hoàn toàn bí mật, hay là vô danh (anonymous), và vai trò của họ là ngang nhau. Cơ chế này loại bỏ nguy cơ các thành viên bồi thẩm đoàn bị lộ danh tính và bị tấn công hay mua chuộc, và qua đó kỳ vọng rằng các quyết định của bồi thẩm đoàn sẽ là công bằng.

Tuy nhiên, nếu ta chẳng biết được bồi thẩm đoàn gồm những ai, số lượng bao nhiêu, thì làm thế nào ghi nhận được quyết định của họ? Bên cạnh đó, còn cần đảm bảo thông tin về quyết định của bồi thẩm đoàn là đích xác và không bị can thiệp? Nội dung này sẽ được tiếp tục trình bày ở những phần tiếp theo.

## Phần 5: Đồng thuận ngang hàng phi tập trung

Satoshi Nakamoto, một hoặc một nhóm người ẩn danh, đã đưa ra cách giải quyết bài toán đồng thuận phi tập trung trong [*đặc tả*](https://bitcoin.org/bitcoin.pdf) (*whitepaper*) về Bitcoin.

Trở lại với lối diễn giải của chúng ta, thay vì lựa chọn bồi thẩm đoàn trước khi phiên tòa diễn ra, chúng ta mang phiên tòa ra quảng trường và công bố bất kỳ ai nếu muốn cũng có thể tới đó tham dự và đưa ra phán quyết của riêng mình, tức là một phiếu bầu (vote). Mỗi phiếu bầu có vai trò ngang nhau, trên đó không ghi danh tính gì hết (*anonymous*). Phán quyết cuối cùng sẽ dựa trên cơ chế đa số (*majority*).

Như vậy, chúng ta chuyển cơ chế đưa ra phán quyết từ chỗ tập trung trong một số nhỏ cá nhân được chỉ định trước, sang cơ chế phi tập trung, tại đó không ai biết trước được sẽ có bao nhiêu người tham gia bầu chọn và cụ thể là những ai. Như thế, kẻ xấu rất khó có thể can thiệp vào kết quả bầu chọn của từng người, dẫn đến khó can thiệp vào phán quyết cuối cùng.

Quay lại với blockchain, khi Bill đưa ra blockchain của hắn, thay vì cử một anh chàng Peter đứng ra đánh giá và xác nhận blockchain của Bill hay một blockchain nào đó là đúng đắn, thì tất cả các blockchain được gửi đến tất cả mọi người: Chris, Leon, Jill, Claire, Ada, Artyom... Mỗi người đều có quyền xem xét và đưa ra bầu chọn của mình. Blockchain nào nhận được nhiều phiếu bầu nhất, sẽ được lựa chọn để tiếp tục sử dụng, các blockchain còn lại sẽ bị tiêu hủy.

Như vậy có vẻ ổn. Thế nhưng nếu Bill phá hoại tiến trình bầu chọn, bằng cách nhanh chóng tạo ra vô số các blockchain khác nhau, hoặc rủ họ hàng hang hốc của hắn tham gia bầu chọn hòng chiếm đa số, thì sao?

Satoshi đã giải quyết khó khăn này bằng cách đưa ra cơ chế *Chứng minh Công việc* (*Proof-of-Work, viết tắt là PoW*). Cơ chế này được trình bày ở phần tiếp theo.

## Phần 6: Proof-of-Work

Như đã nói cuối phần trước, có 2 khả năng Bill sẽ can thiệp cuộc bầu chọn blockchain, một là nhanh chóng tạo ra vô số các blockchain nhằm làm nhiễu loạn quá trình bầu chọn, hai là rủ anh em nhà hắn tới tham gia bầu chọn hòng chiếm đa số. Thậm chí hắn có thể sử dụng cùng lúc cả 2 cách.

Nhưng nếu ta yêu cầu rằng, mỗi người, để tạo ra một block mới, phải vác đủ 100 viên gạch đến quảng trường trung tâm để sung vào quỹ xây dựng nhà tình nghĩa, thì sao? Để sửa block C, Bill phải vác tới 100 viên, rồi block D, block E nữa, để tạo ra blockchain "đểu" đầu tiên, Bill đã phải vác đến quảng trường tới 300 viên gạch. Chưa kể, hắn không thể cùng lúc vác đến 300 viên. Khỏe mấy, hắn cũng chỉ có thể vác được 50 viên mỗi lần, và phải đi mất đến 1 tiếng đồng hồ từ lò gạch đến quảng trưởng. Để hoàn thành blockchain đểu đầu tiên, tổng cộng hắn mất 300 viên gạch cùng với 6 tiếng đồng hồ. Như vậy đủ khiến Bill phát hoảng khi nghĩ đến việc tiếp tục tạo ra thêm những blockchain đểu khác để làm rối cuộc bình bầu.

Bên cạnh đó, ta cũng yêu cầu rằng, vị nào muốn tham gia bầu chọn, cũng phải làm như Bill. Và ta lại bổ sung thêm rằng, giá trị của một phiếu bầu sẽ được tính trên số lượng gạch mà phiếu đó đại diện. Như thế, Bill có thể rủ thêm anh em hắn đến tham gia, nhưng mỗi người đều phải mất rất nhiều công sức và thời gian để vác đủ số gạch tới quảng trường hòng chiếm đa số. Vì thế, rất ít hoặc thậm chí không ai thèm quan tâm tới đề nghị của Bill. Đơn giản là việc mang được số lượng gạch đủ để chiếm đa số so với cả đám đông ngoài kia, đối với Bill và đồng bọn của hắn, là không thể.

Nói một cách khác, ta bắt mỗi người phải chứng minh rằng anh đã thực sự bỏ công sức ra để xứng đáng giành quyền tạo lập blockchain cũng như bình chọn nó. Giới hạn về khả năng làm việc của anh so với đám đông, chính là giới hạn khả năng phá hoại hoặc can thiệp có chủ đích của anh đến blockchain.

Đó là cách diễn giải đơn giản về cơ chế Proof-of-Work mà Satoshi Nakamoto đã đưa ra để hiện thực hóa đồng tiền số dựa trên blockchain đầu tiên của thế giới: Bitcoin.

Phần tiếp theo sẽ đi sâu hơn vào nội dung kỹ thuật của PoW.

## Phần 7: PoW và độ khó của blockchain

*Phần này có thể bỏ qua nếu bạn không quá quan tâm đến khía cạnh kỹ thuật của cơ chế PoW*

Ngay tại Phần 1, ta đã biết rằng một block cần phải chứa hash của block trước nó. Thuật toán hash mà Satoshi đưa ra với Bitcoin là SHA-256, nó tạo ra một hash 256 byte từ dữ liệu đầu vào. Thuật toán SHA-256 chạy rất nhanh, một máy tính cá nhân thời nay chỉ mất 1 giây để mã hóa hơn 3 Gigabyte dữ liệu với thuật toán này, trong khi đó kích thước block phiên bản đầu tiên của Bitcoin chỉ là 1 MB. Nghĩa là chỉ mất 0,0003 giây để tính hash của 1 block.

Để tăng khối lượng tính toán khi tạo lập một block, Satoshi yêu cầu mỗi *điểm tính toán* (*node*), cần đưa vào block một con số ngẫu nhiên, gọi là *nonce* (*number used once*), trước khi tính hash cho block đó, và để đủ điều kiện xem xét đưa vào blockchain, hash của block này (gồm cả nonce) phải là một chuỗi bắt đầu bởi N bits có giá trị bằng 0 (zero).

*Bit là đơn vị dữ liệu nhỏ nhất trong khoa học máy tính, nó chỉ có thể chứa một trong hai giá trị là "0" hoặc "1".*

Ta biết rằng chỉ cần dữ liệu đầu vào thay đổi một bit, thì chuỗi hash đầu ra sẽ thay đổi hoàn toàn, và rất ngẫu nhiên. Tuy rằng dữ liệu của block cần tạo lập không thay đổi, nhưng vì có thêm nonce, và với mỗi giá trị khác nhau của nonce, mà hash của block thay đổi rất nhiều.

Do đó, để tìm được một nonce thỏa mãn điều kiện có N zero bits ở đầu chuỗi hash, cần rất nhiều công sức tính toán của máy tính. Cách duy nhất để tìm ra nonce phù hợp là cho nó tăng dần từ 0 cho đến khi hash đầu ra thỏa mãn điều kiện.

Điều kiện nói trên được gọi là *độ khó* (*difficulty level*) của blockchain. Để được coi là block hợp lệ, giá trị hash của nó phải nhỏ hơn độ khó hiện tại của blockchain. Bên cạnh đó, độ khó này có thể được điều chỉnh tùy vào trạng thái của toàn bộ blockchain, nhằm đảm bảo tính bền vững của nó.

Trên thực tế, sẽ xảy ra trường hợp gần như cùng một thời điểm, có nhiều node cùng tìm ra các nonce thỏa mãn độ khó yêu cầu. Vậy ta sẽ lựa chọn block do node nào giới thiệu?

Nội dung này sẽ được trình bày ở phần tiếp theo.

## Phần 8: Longest chain

Khi một node tạo ra một block hợp lệ, nó sẽ thông báo cho tất cả node khác trong *mạng lưới* (*network*) blockchain. Sẽ luôn xảy ra trường hợp gần như cùng một lúc, một node sẽ nhận được những block mới từ những node khác nhau. Khi ấy, nó sẽ chọn block đầu tiên để đưa vào blockchain của mình và tiếp tục làm việc để tạo lập block tiếp theo. Tuy nhiên, các block đến sau vẫn được nó lưu lại để dự phòng. Đến khi block tiếp theo được tạo lập, một trong các nhánh (branch) của blockchain sẽ trở nên dài hơn các nhánh còn lại. Theo nguyên tắc, node này sẽ chấp nhận đi theo *nhánh dài nhất* (*longest branch/chain*), tức là có số lượng block hợp lệ lớn nhất, đồng nghĩa với khối lượng công việc đã thực hiện nhiều nhất. Các block thuộc những nhánh còn lại, mặc dù hợp lệ (thỏa mãn độ khó) sẽ bị loại bỏ, và chúng được gọi là *uncle block* (so sánh với *parent block*, là block nằm trước trên nhánh chính).

Ví dụ, blockchain hiện là A-B-C-D-E, và trong khi đang tìm nonce cho block mới là F, thì Chris gần như đồng thời nhận được từ Leon và Jill 2 block mới hợp lệ (có nonce khác nhau, nhưng hash tổng vẫn thỏa mãn độ khó) gọi là F1 và F2. Chris sẽ dừng việc tìm F, chấp nhận sử dụng block F1 của Leon như block mới (dù nó chỉ đến trước Jill vài phần trăm giây), và lưu block F2 của Jill lại để dự phòng. Như vậy, trong tay Chris đang có 2 chain sau: "A-B-C-D-E-F1" (chain chính) và "A-B-C-D-E-F2" (chain dự phòng). Gộp lại ta có hình ảnh của một cành cây 2 nhánh, chia tách từ sau block E. Sau đó Chris tiếp tục tìm kiếm block mới (G) trên nhánh Leon.

Tuy nhiên, vì lý do nào đó, Ada lại nhận được F2 của Jill trước F1 của Leon và bắt đầu tìm kiếm block G trên nhánh Jill, ngược lại so với Chris.

Sau một thời gian, Ada là người đầu tiên tìm được block G. Cô ta gửi nó đến toàn bộ mạng lưới. Vì trong một khoảng thời gian đủ dài, chưa có ai tìm được block G ngoài Ada, nên tất cả đều chấp nhận block G do Ada tìm ra. Và vì Ada tìm ra block G trên nhánh Jill, nên giờ đây nhánh của Jill (A-B-C-D-E-F2-G) dài hơn so với nhánh của Leon (A-B-C-D-E-F1). Do đó, Chris buộc phải chuyển từ nhánh anh ta đang làm việc (nhánh Leon) sang nhánh của Jill. Cũng may, là Chris vẫn còn lưu giữ block F2 của Jill làm dự phòng, nên giờ đây anh ta có thể chuyển sang nhánh Jill một cách dễ dàng, và sau đó chỉ việc bổ sung thêm block G của Ada là xong.

Đến đây, ta đã đi qua những phần cơ bản nhất của blockchain. Ở phần tiếp theo, ta sẽ bàn thêm về ý nghĩa các giải pháp mà Satoshi đem lại cho Bitcoin.

## Phần 9: Sổ cái và Bitcoin

Kết hợp thiết kế của blockchain, cơ chế đồng thuận ngang hàng phi tập trung, và cơ chế Proof of Work được trình bày ở các phần trước, mang lại các đặc trưng sau:

- Tính toàn vẹn: dữ liệu trên các block đã có trên blockchain là vĩnh viễn không thể thay đổi và và có thể kiểm tra dễ dàng.
- Tính công khai: bất kỳ ai cũng có thể truy xuất toàn bộ blockchain bất cứ lúc nào.
- Tính đúng đắn: không ai có thể can thiệp thay đổi nội dung blockchain sai với thực tế để làm lợi cho riêng mình.

Với những đặc trưng trên, blockchain rất thích hợp để ứng dụng vào một việc, đó là ghi lại các giao dịch. Nói cách khác, một blockchain chính là một cuốn *sổ cái* (*ledger*) tương tự như sổ cái dùng trong công tác kế toán tại các công ty. Chính vì vậy, ứng dụng blockchain mà Satoshi Nakamoto đã đưa ra trong đặc tả của mình chính là một loại *tiền số hóa*, được đặt tên là *Bitcoin*. Cái tên này có lẽ là sự kết hợp giữa chữ "bit", là đơn vị dữ liệu nhỏ nhất trong khoa học máy tính, và "coin", tức là đồng xu. Đơn vị tiền tệ biểu diễn giá trị các giao dịch trong "sổ cái" Bitcoin được quy định là "bitcoin", viết tắt là *BTC*. Ví dụ: trong một block nào đó của blockchain Bitcoin ghi rằng *"Chris chuyển cho Leon một giá trị là X"*, thì ta hiểu rằng *"X"* ở đây là *"X bitcoin"* hay *"X BTC"*. Thực tế thì hiện nay, do giá trị của một bitcoin rất lớn (~ 41.000 USD), nên người ta sử dụng *satoshi* (viết tắt là *sat*) để ghi nhận giá trị các giao dịch bitcoin trong blockchain. 1 satoshi = 0,00000001 BTC (một phần trăm triệu bitcoin).

Điểm khác biệt của "sổ cái" Bitcoin với sổ cái thông  thường đó là tính công khai, một trong 3 đặc trưng, như ta đã nói ở trên. Bất kỳ ai cũng có thể xem toàn bộ lịch sử giao dịch trên Bitcoin. Tuy nhiên, Satoshi đã đưa vào Bitcoin một thiết kế dữ liệu giao dịch, qua đó đem lại cho nó một đặc trưng nữa, đó là tính *vô danh* (*anonymity*). Trong dữ liệu một giao dịch của Bitcoin, không có danh tính của người gửi và người nhận, mà chỉ có các chuỗi địa chỉ trông có vẻ như là những chuỗi số và chữ cái ngẫu nhiên, và người ta gọi chúng là các *địa chỉ ví* (*wallet address*) Bitcoin.

Ví và giao dịch Bitcoin sẽ được làm rõ hơn ở các phần tiếp theo.

## Phần 10: Giao dịch và xác minh giao dịch

*Đây là một trong những phần có thể nói là khó hiểu và quan trọng nhất khi tìm hiểu cách thức hoạt động của Bitcoin.*

Trước hết, cần phải hiểu cách mà Bitcoin xác minh và thực hiện các giao dịch gửi tiền (bitcoin) đến cho ta cũng như các giao dịch mà ta chuyển tiền cho người khác.

Giả sử Chris cần chuyển cho Leon 50 BTC và cho Jill 40 BTC. Anh ta sẽ nói với mọi người thế nào? Có phải là: *"Này mọi người, tôi sẽ chuyển 50 cho Leon, và 40 cho Jill"*? OK được thôi. Vấn đề là, *Chris có đủ tiền để chuyển đi số tiền trên hay không*?

Thông thường, khi có phát sinh giao dịch gửi hay nhận tiền, các hệ thống kế toán sẽ ghi nhận giao dịch, tính toán *số dư* (*balance*), rồi lưu số dư này lại để tính toán cho các giao dịch tiếp theo. Không nhất thiết phải tính toán và ghi nhận số dư sau mỗi giao dịch, nhưng thường việc này sẽ được thực hiện theo kỳ, ví dụ cuối ngày hay cuối tháng. Lý do của cách làm này, là để tăng tốc độ xử lý giao dịch. Thay vì phải cộng trừ tất cả các giao dịch từ đầu của cả hệ thống cho đến trước giao dịch cần thực hiện, để xem số dư còn đáp ứng hay không, thì hệ thống chỉ cần làm thế với các giao dịch từ đầu kỳ. Dù sao, tính toán số lượng giao dịch của một vài ngày vẫn nhanh hơn là vài năm, phải không?

Tuy nhiên, phương pháp trên tiềm ẩn rủi ro rất lớn. Chris có thể sinh ra tham lam, và tìm cách sửa số dư đầu kỳ của anh ta để có nhiều tiền hơn. Vì hệ thống chỉ xác minh giao dịch dựa trên số dư đầu kỳ, nên Chris chỉ cần can thiệp vào con số này và một số lượng nhỏ giao dịch trước đó trong kỳ. Như thế rõ ràng là đỡ tốn công sức hơn là phải chỉnh sửa toàn bộ các giao dịch từ đầu hệ thống.

Với tầm nhìn về một hệ thống xử lý giao dịch công khai theo mô hình mạng phân tán ngang hàng có quy mô toàn cầu, Bitcoin cần phải được thiết kế sao cho rủi ro bị tấn công, sửa đổi là thấp nhất. Vì thế, trong Bitcoin, chẳng có cái gì gọi là số dư cả.

Vậy nếu Chris muốn chuyển 50 BTC cho Leon và 40 BTC cho Jill, thì anh ta làm thế nào để thuyết phục mọi người là anh ta có đủ ít nhất 90 BTC để thực hiện 2 giao dịch trên? Vì nếu anh ta không chứng minh được rằng anh ta đang có ít nhất 90 BTC trong tay, thì mạng lưới Bitcoin, tức là những người khác: Leon, Jill, Ada, Claire, Artyom..., sẽ không chấp nhận 2 giao dịch mà anh ta đang muốn tiến hành.

*Trong Bitcoin blockchain, mọi giao dịch đều được định danh bởi một chuỗi mã số, gọi là mã số định danh giao dịch (Transaction's Identification - TXID). Ta sẽ nói một cách ngắn gọn là mã giao dịch. Khi một giao dịch được chấp nhận vào ghi vào blockchain, thì cả dữ liệu của giao dịch lẫn mã giao dịch của nó đều được lưu giữ.*

Và đây là cách mà Chris làm để thuyết phục mọi người rằng anh ta có đủ tiền để thực hiện 2 giao dịch mong muốn. Anh ta cung cấp cho mọi người một danh sách các mã số giao dịch trước đó (đã được ghi trên blockchain), trong đó Chris là người được nhận tiền. Ví dụ, Chris bảo: *"Này mọi người, trước đây Ada và Artyom đã chuyển cho tôi một số tiền, mã giao dịch của chúng là TXID1 và TXID2, và bây giờ, tôi sẽ chuyển cho Leon 50 BTC, và chuyển cho Jill 40 BTC"*. Những giao dịch mà Chris liệt kê trong đó anh ta là người nhận tiền, được gọi là các *giao dịch đầu vào* (*input transaction*s), ở đây là *TXID1* và *TXID2*. Mọi người sẽ rà soát trên blockchain để tìm kiếm 2 giao dịch có mã số *TXID1* và *TXID2*, sau đó kiểm tra nội dung các giao dịch này, mục đích là để trả lời các câu hỏi sau:

1. Các giao dịch đầu vào này có tồn tại trên blockchain không?
2. Các giao dịch trên có đúng là chuyển tiền cho Chris không?
3. Số tiền của mỗi giao dịch trên là bao nhiêu?
4. Tổng số tiền Chris nhận được từ các giao dịch trên có đủ để anh ta thực hiện các giao dịch chuyển tiền đi hay không?

Nếu tất cả các câu trả lời là đúng, thì giao dịch của Chris sẽ được *chấp nhận* (*verified*) và sẽ được ghi vào blockchain.

Ở đây ta thấy rằng để kiểm tra một giao dịch mới, mọi người phải rà soát toàn bộ các transactions trong cả blockchain. Tại thời điểm viết bài này, tổng số giao dịch của Bitcoin đã lên tới gần 680 triệu, và trung bình có tới hơn 260 nghìn giao dịch mới mỗi ngày. Như vậy, việc xác minh giao dịch hẳn nhiên phải trở nên rất chậm chạp và hạn chế khả năng mở rộng của Bitcoin. 

Phải có cách nào đó tốt hơn để khắc phục vấn đề này. Giải pháp đó sẽ được trình bày ở phần tiếp theo.

## Phần 11: UTXO

Ở cuối phần trước, ta đã đặt ra vấn đề làm thế nào để giảm tải cho việc xác minh các giao dịch, khi mỗi người đều phải rà soát gần như toàn bộ các giao dịch đã có trên blockchain để xác minh một giao dịch mới.

Trở lại với ví dụ của chúng ta. Mọi người đều đã xác nhận giao dịch của Chris là OK và giao dịch này sẽ được ghi vào blockchain. Ta đã biết rằng giao dịch này liệt kê 2 giao dịch đầu vào là TXID1 và TXID2, và ta đặt cho giao dịch mới được ghi nhận của Chris là TXID3. Tại thời điểm này, rõ ràng là vai trò cung cấp dòng tiền vào của TXID1 và TXID2 đã hết, vì toàn bộ số BTC của 2 giao dịch này đã đi vào giao dịch TXID3 do Chris mới tạo ra. Với Bitcoin, chúng được coi là những *"giao dịch đã được sử dụng"* (*spent transaction*). Theo nguyên tắc của Bitcoin, *một giao dịch chỉ có thể được sử dụng một lần duy nhất*. Trong trường hợp khi TXID3 của Chris được chấp thuận, thì TXID1 và TXID2 đều đã được sử dụng, và không giao dịch nào khác được sử dụng chúng làm giao dịch đầu vào nữa. Và vì thế, không ai còn quan tâm đến 2 giao dịch này nữa. Tất cả sẽ bỏ qua 2 giao dịch có mã số TXID1 và TXID2 trong khi rà soát trên blockchain. Bằng cách đó, Bitcoin giảm đáng kể số lượng giao dịch cần rà soát khi xác minh một giao dịch mới.

Nhưng việc cải tiến chưa dừng lại ở đó!

Ở trên, ta biết rằng TXID1 và TXID2 đã được sử dụng, và chẳng ai cần đến chúng nữa trong quá trình xác minh giao dịch đầu vào. Tiếp tục với ví dụ của chúng ta: TXID3 là mã giao dịch của Chris, trong đó TXID1 và TXID2 là 2 giao dịch đầu vào, cung cấp dòng tiền vào cho Chris để anh ta yêu cầu 2 giao dịch mới để chuyển tiền cho Leon và Jill. Hãy tạm gọi 2 giao dịch này là TXID4 và TXID5. Tại thời điểm TXID3 được ghi nhận vào blockchain, TXID4 chứa 50 BTC, còn TXID5 chứa 40 BTC. Số tiền này đều chưa được ai sử dụng. Chúng được gọi là *"số tiền đầu ra chưa được sử dụng"* (*Unspent Transaction Ouput - UTXO*). Thuật ngữ này rất khó dịch cho thoát, nên từ giờ ta sẽ gọi chúng đơn giản là UTXO. Chỉ các UTXO mới được sử dụng để làm đầu vào cho các giao dịch. Điều này rất dễ hiểu: *anh chỉ có thể sử dụng số tiền anh chưa sử dụng mà thôi*.

UTXO có vai trò vô cùng quan trọng trong thiết kế của Bitcoin. Mỗi node trong mạng lưới Bitcoin đều có một bảng theo dõi các UTXO này (được gọi là *tập hợp UTXO*, *UTXO set*) và cập nhật nó sau mỗi giao dịch. Thay vì phải rà soát trên blockchain để xác minh các giao dịch, các node chỉ cần rà soát trên UTXO set, sẽ nhanh hơn rất nhiều. Một phần vì kích thước dữ liệu của UTXO nhỏ hơn và đơn giản hơn block, một phần vì số lượng các UTXO có thể giảm đi sau một giao dịch. Đó là trường hợp số UTXO được sử dụng để cung cấp dòng tiền vào của một giao dịch lớn hơn số UTXO phát sinh sau giao dịch. Giả sử trong TXID3, Chris chỉ chuyển tiền cho Leon, mà không chuyển cho Jill, như thế sau khi giao dịch được thực hiện, 2 UTXO của TXID1 và TXID2 đã được tiêu thụ, và chỉ phát sinh 1 UTXO mới mà thôi. Do vậy, số lượng UTXO cần theo dõi trong UTXO set đã giảm đi 1. Trong khi với thời gian, kích thước blockchain chỉ có tăng chứ không giảm, thì kích thước UTXO set có thể dao động quanh một khoảng nhỏ hơn nhiều. Trong khi hiện nay tổng kích thước blockchain của Bitcoin đã lên tới hơn 350 Gigabyte, thì kích thước trung bình của UTXO set chỉ khoảng 3.5 Gigabyte, hoàn toàn đủ nhỏ để chứa hẳn trong bộ nhớ máy tính, qua đó tăng đáng kể tốc độ xác minh giao dịch của node.

***Lưu ý:***

- *Việc lưu trữ, quản lý UTXO set này là việc riêng của mỗi node. UTXO set không được lưu trên blockchain.*
- *Thực tế cấu trúc dữ liệu cũng như cách thức xử lý các giao dịch và UTXO của Bitcoin phức tạp hơn rất nhiều.*

## Phần 12: Tiền thừa, phí giao dịch và coinbase

Quay trở lại ví dụ giao dịch của Chris, ta để ý rằng 2 UTXO đầu vào cung cấp cho nó 100 BTC (50 từ Ada và 50 từ Artyom), nhưng đầu ra chỉ có 90 BTC mà thôi (50 cho Leon, 40 cho Jill). Vậy còn 10 BTC thừa ra (change) thì xử lý ra sao?

Bitcoin không tự động ghi nhận 10 BTC tiền thừa này lại cho Chris. Ta nhớ ở Phần 10 đã nói rằng Bitcoin không có khái niệm số dư. Mọi con số trên Bitcoin đều phải tính toán từ các giao dịch và các UTXO. Nếu vậy, Chris sẽ bị mất toi 10 BTC hay sao?

Dĩ nhiên Chris không muốn thế. Cho nên anh ta bổ sung thêm 1 nội dung nữa trong giao dịch của mình, đó là chuyển 10 BTC ngược trở lại cho mình. Như thế, sau khi thực hiện giao dịch TXID3, ta có 3 UTXO mới như sau:

1. 50 BTC cho Leon.
2. 40 BTC cho Jill.
3. *10 BTC cho chính Chris.*

Việc chuyển lại tiền cho chính mình nghe rất khôi hài với hầu hết mọi người, nhưng nó rất có lý với Bitcoin. Bởi vì Bitcoin không phải đẻ thêm ra một cơ chế khác để quản lý số dư, mà lý do thì ta đã biết: số dư là một điểm rủi ro về an ninh, rất dễ bị tấn công khai thác.

Trở lại với Chris. Trong lúc lập giao dịch, anh ta nghĩ rằng, có lẽ nên khuyến khích mọi người tham gia vào xử lý giao dịch của anh ta. Như thế mọi người sẽ nỗ lực hơn và vì thế giao dịch của anh ta sẽ được thực hiện nhanh hơn. Chris đang rất vội! Nhưng khích lệ mọi người bằng cách nào? Thôi thì để lại 1 BTC cho bất cứ ai đưa được giao dịch này vào blockchain. Vì thế, Chris điều chỉnh giao dịch chuyển tiền như sau:

1. 50 BTC cho Leon.
2. 40 BTC cho Jill.
3. 9 BTC cho chính Chris.

Như thế, còn thừa ra 1 BTC. Bitcoin có quy định rằng, nếu sau một giao dịch mà có một lượng tiền thừa, không thuộc vào một UTXO nào, thì nó sẽ chuyển số tiền thừa đó cho người nào có công đưa được giao dịch đó vào blockchain (tức là người tạo ra được block mới, trong đó chứa giao dịch này, và block đó được ghi nhận vào blockchain). Khoản tiền này được gọi là *phí giao dịch* (*transaction fee*).

Khoản phí này được chuyển đến người có công tạo block thế nào? Bitcoin cho phép người tạo block đưa vào đầu danh sách của giao dịch của block một giao dịch đặc biệt, được gọi là *coinbase* transaction. Người được nhận tiền từ giao dịch coinbase chính là người tạo block, còn giá trị là tổng số tiền phí giao dịch từ tất cả các giao dịch trong block, cùng với 1 khoản thưởng đặc biệt, gọi là *block reward*. Ta sẽ bàn về block reward ở phần sau. Như vậy, nếu may mắn đến với Ada, và block của cô ấy được chấp nhận, thì Ada sẽ có thêm được một UTXO với số tiền ghi trong coinbase của block.

Phần tiếp theo sẽ bàn về block reward và cơ chế đào (mining) bitcoin.

## Phần 13: Block reward, halving, thợ đào và pool

Khởi đầu của Bitcoin, trong mang lưới không có lấy một satoshi nào. Lượng tiền số lưu hành trên nó là con số 0 tròn trĩnh.

Để phát hành tiền bitcoin đưa vào lưu hành, nhóm phát triển Bitcoin đưa ra cơ chế đào (mine) bitcoin như sau:

- Với mỗi block mới được ghi vào blockchain, người tạo block đó được thưởng một lượng bitcoin mới (chưa có trên mạng lưới). Có thể hiểu lượng bitcoin "đào" được này như việc in thêm tiền. Phần thưởng này được gọi là "*block reward*".
- Những người chạy các node (các máy tính) để tham gia vào việc tính toán, xác minh giao dịch, tạo lập các block, được gọi là các "*thợ mỏ*" hay "*thợ đào*" (*miner*).
- Để kìm chế lạm phát, cứ mỗi 210.000 block, Bitcoin giảm số lượng block reward đi một nửa, goi là *halving*. Bitcoin được thiết kế để ra một block mới mỗi 10 phút. Như thế, sau khoảng mỗi 4 năm thì phần thưởng cho "thợ đào" lại giảm đi một nửa. Năm 2008, khi mới đi vào hoạt động, block reward là 50 BTC (Satoshi chính là người được hưởng phần thưởng 50 BTC đầu tiên khi tạo ra block zero, hay còn gọi là *genesis block*). Đến 2012, phần thưởng còn 25 BTC. Năm 2016, là 12,5 BTC. Và tại thời điểm viết bài này, năm 2021, phần thưởng này chỉ còn 6,25 BTC. Với quy định này, đến năm 2137, sẽ không còn phần thưởng nào cho thợ đào nữa, và số lượng BTC của Bitcoin dừng lại ở con số xấp xỉ 21 triệu BTC.
- Xác suất để một thợ đào may mắn tạo được một block mới trên blockchain của Bitcoin để nhận block reward tỉ lệ theo phần trăm năng lực tính toán của node do anh ta vận hành so với tổng năng lực tính toán của toàn mạng lưới. Năng lực tính toán này được đo theo số lượng hash tính được trong một giây (xem [Phần 6](#proof-of-work)), và thường được ghi là Gh/s (Gigahash trên giây, 1 Gh = 1 tỷ hash). Hiện tại, tổng công suất tính toán của của mạng lưới Bitcoin là khoảng 122,77 M TH/s (122,77 tỷ Gh/s, hay là 122,77 x 10<sup>18</sup> H/s). Để hình dung, một máy tính để bàn sử dụng loại CPU phổ biến hiện nay là Intel Core i5 có công suất tính toán khoảng 800 H/s.
- Vì khả năng để một thợ đào riêng lẻ đào được block reward là rất thấp, nên rất nhiều thợ đào đang cùng tham gia vào một hình thái hợp tác xã, gọi là mining pool, để cùng nha đào bitcoin. Khi một máy tính trong pool may mắn đào được một lượng bitcoin, một phần của phần thưởng đó sẽ được chia cho những người khác theo tỉ lệ đóng góp công suất tính toán chung của pool. Như thế, thu nhập của mỗi thợ đào sẽ ổn định hơn.

## Phần 14: Ví, chữ ký, và chùm chìa khóa

Trong [Phần 9](#phần-9-sổ-cái-và-bitcoin), ta đã nói rằng địa chỉ nhận tiền trong các giao dịch của Bitcoin là một chuỗi chữ và số có vẻ ngẫu nhiên và được gọi là địa chỉ ví Bitcoin. Chúng giúp che giấu danh tính của người nhận, tạo nên đặc tính vô danh, một trong những đặc tính cốt lõi của nền tảng Bitcoin.

Khi ta muốn nhận hay gửi tiền qua ngân hàng, trước tiên, ta cần mở tài khoản. Khi ta chuyển tiền đi, hoặc khi có ai đó chuyển tiền cho ta, thì số tài khoản của người nhận cần được ghi vào trong lệnh chuyển tiền. Số tài khoản này, thực chất, được ánh xạ vào trong một cơ sở dữ liệu tập trung của ngân hàng, tại đó lưu giữ rất nhiều thông tin định danh của người nhận: tên, ngày sinh, giới tính, địa chỉ thường trú, số chứng minh nhân dân... Như vậy, cơ chế quản lý tài khoản của ngân hàng hoàn toàn không phải là cơ chế vô danh. Điều này là cần thiết với hoạt động của ngân hàng, nhưng nó tạo ra rủi ro xâm phạm quyền riêng tư của khách hàng.

### Ví

Với Bitcoin, ta cũng cần có tài khoản, hay gọi một cách thông dụng hơn trong giới tiền số (Bitcoin là một loại tiền số, cryptocurrency), là ví (wallet). Có lý do cho cách gọi này. Đó là tài khoản thường gắn với thông tin định danh, còn ví thì không. Anh có thể nhét chứng minh thư, bằng lái xe... vào ví, và khi đó cái ví không chỉ chứa tiền, mà còn chứa thông tin định danh người sở hữu ví, và có thể nói, khi đó nó có tính chất của một tài khoản. Nhưng dĩ nhiên, không ai bắt anh phải nhét giấy tờ nhân thân vào ví, khi đó, nó chỉ có mỗi một việc là chứa tiền của anh. Nếu anh đánh rơi ví, người khác nhặt được nó, họ sẽ không biết nó thuộc về ai cả. Khi đó, ví mang tính chất vô danh. Do vậy, ví là một thuật ngữ phù hợp hơn để sử dụng trong bối cảnh của Bitcoin, và các đồng tiền số tương tự.

Trên một lệnh chuyển tiền ngân hàng (chỉ xét trường hợp trong cùng ngân hàng), ta thấy có 3 thông tin quan trọng:

- Số tài khoản người nhận.
- Số tiền.
- Chữ ký của người gửi.

Trong đó, quan trọng nhất là chữ ký của người gửi, tức chủ tài khoản. Nếu chữ ký không đúng với mẫu đã đăng ký cho tài khoản, lệnh chuyển tiền này sẽ bị từ chối xử lý ngay lập tức.

Trở lại với ví dụ của chúng ta. Với Bitcoin, không có cái gì gọi là thông tin tài khoản, mẫu chữ ký. Vậy thì Chris ký xác nhận lệnh chuyển tiền, tức giao dịch TXID3, thế nào? Làm sao để những người khác xác minh lệnh này do chính Chris đưa ra?

Ở đây, ta cần chấp nhận tìm hiểu thêm một khái niệm mới có tính kỹ thuật một chút: đó là *"chìa khóa"* (*key*). Mà thực ra là 2 loại chìa: *chìa công khai* (*public key - PK*) và *chia riêng tư* (*secret/private key - SK*).

### Chữ ký

Giới khoa học máy tính từ lâu đã phát minh ra một số thuật toán, được gọi là mã hóa khóa công khai (Public Key Cryptoghraphy - PKC). Đặc điểm của phương thức mã hóa này là *bất đối xứng* (*asymetric*). Điều đó có nghĩa là sao?

Thông thường, khi cần mã hóa dữ liệu, ta sẽ sử dụng một cụm từ ngữ, khi kết hợp nó với thuật toán mã hóa, sẽ mã hóa dữ liệu đầu vào thành một khối dữ liệu đầu ra khác hẳn và vô nghĩa. Muốn giải mã khối dữ liệu đầu ra này, ta cần cụm từ ngữ kia, cho chạy qua thuật toán để giải mã ngược lại. Đây là phương thức mã hóa đối xứng (symetric). Để mã hóa hay giải mã, ta chỉ cần sử dụng cùng một cụm từ ngữ, đó chính là chìa khóa để mã hóa và giải mã.

Với PKC thì khác hẳn. PKC sinh ra không phải một, mà là một cặp chìa khóa, bao gồm một khóa công khai (Public Key) và một khóa riêng tư (Secret Key - SK). Dữ liệu bị mã hóa bởi khóa riêng tư chỉ có thể được giải mã bởi khóa công khai tương ứng. Tại sao lại có cái gọi là công khai và riêng tư này? Hai cái tên đó xuất phát từ ý nghĩa sử dụng của mỗi loại khóa. Khóa công khai, là chìa mà ta công khai chia sẻ cho những người khác, còn khóa riêng tư, là chìa mà ta giữ bí mật cho riêng mình. Mục đích làm như vậy làm để làm gì? Ta xét ví dụ sau:

Chris gửi cho Ada một bức thư. Vì trong quá trình chuyển phát, một kẻ trung gian nào đó, ví dụ chính tay bưu tá, có thể đọc trộm, và thậm chí thay đổi nội dung bức thư (giả mạo), cho nên Chris cần một phương thức nào đó để đảm bảo 2 mục tiêu:

1. Mã hóa nội dung thư, và chỉ người nhận đích danh (Ada) mới giải mã được.
2. Người nhận thư yên tâm rằng nội dung thư không bị sửa đổi, và nó thực sự đến từ người gửi đích danh (Chris).

Để làm được như vậy, Chris sử dụng thuật toán PKC tạo ra một cặp khóa riêng tư (SK) và khóa công khai (PK). Anh ta dùng SK để mã hóa nội dung thư, và nhắn tin cho Ada biết PK của mình. Khi tay bưu tá mở bức thư của Chris ra, hắn thấy một mớ ký tự hỗn độn, không tài nào hiểu được, và Chris đạt mục tiêu thứ nhất. Sau đó, thư đến tay Ada. Cô ấy thấy bức thư đề người gửi là Chris, vì vậy, cô ấy tìm lại trong các tin nhắn cái PK từ Chris, và thử giải mã bức thư với PK này. Nếu Ada giải mã thành công, thì cô ấy sẽ đọc được nội dung thư, đồng thời yên tâm rằng thư này đúng là từ Chris. Nếu Ada không giải mã được, nghĩa là bức thứ này không phải đến từ Chris.

Như vậy, với PKC, ta có được trong tay phương thức mã hóa vừa đảm bảo bảo mật dữ liệu, lại vừa có khả năng xác minh nguồn gốc của nó.

Trở lại với bài toán xác minh lệnh chuyển tiền. Chris hoàn toàn có thể áp dụng cùng phương pháp với gửi thư. Anh ta có thể dùng SK để mã hóa nội dung chuyển tiền, và thông báo PK tương ứng cho tất cả mọi người, để mọi người có thể dùng PK đó để giải mã lệnh chuyển tiền, qua đó xác nhận lệnh này đúng là của Chris, và sau đó xác minh nội dung chuyển tiền là hợp lệ (ví dụ số dư hiện có của Chris đủ để chuyển tiền đi). Tuy nhiên, phương pháp này có một nhược điểm: nó làm lộ danh tính của Chris, vì mọi người biết PK này là của anh ta.

Với Bitcoin, mọi người không cần quan tâm ai là người tạo giao dịch, ai là người nhận. Như thế mới đảm bảo tính vô danh của mạng lưới. Nhưng việc xác minh giao dịch hợp lệ vẫn phải được tiến hành. Vậy giải quyết vấn đề này ra sao? 

Satoshi đưa ra ý tưởng như sau: với mỗi giao dịch chuyển tiền đi, người lập giao dịch sẽ lấy nội dung giao dịch, chạy nó qua thuật toán hash, rồi sử dụng SK của mình để mã hóa chuỗi hash, và sinh ra một mẩu dữ liệu, được gọi là chữ ký số (digital signature) của giao dịch. Thao tác sử dụng SK để mã hóa vừa nói chính là thao tác ký nhận dữ liệu (signing). Người lập giao dịch sẽ đính kèm chữ ký này vào dữ liệu giao dịch, và gửi lên mạng lưới. Như vậy, dữ liệu của một giao dịch mới sẽ gồm:

1. Danh sách giao dịch đầu vào (TXID1, TXID2).
2. Địa chỉ người nhận và số tiền cần chuyển (50 BTC cho Leon, và 40 cho Jill).
3. Chữ ký số của Chris.

Lưu ý là ở nội dung (2) trên đây, thay vì 2 cái tên Leon và Jill, thì Chris điền vào đó 2 PK, một là của Leon, và PK còn lại là của Jill. Vì sao anh ta lại biết PK của Leon và Jill? Là vì chính Leon và Jill đã cung cấp cho Chris. Trước khi chuyển tiền, Chris nhắn tin cho Leon và bảo *"Này Leon, anh sẽ chuyển cho chú 50 BTC, chú đưa anh cái địa chỉ ví của chú để anh vào lệnh"*, và Leon sẽ trả lời: *"OK Chris, anh chuyển vào ví có địa chỉ **1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2** nhé"*. Chuỗi ký tự rắc rối trong tin nhắn của Leon chính là địa chỉ ví của anh ta, và nó chính là PK của Leon. Tương tự, Jill sẽ chuyển cho Chris địa chỉ ví của mình, tức là PK của cô ấy. Như vậy, nội dung giao dịch của Chris chính xác là như sau:

1. Danh sách giao dịch đầu vào (TXID1, TXID2).
2. Địa chỉ ví (PK) của người nhận và số tiền cần chuyển.
3. Chữ ký số của Chris.

Toàn bộ nội dung trên sẽ được đưa lên mạng lưới để mọi người cùng biết. Bây giờ, để xác minh giao dịch TXID3 của Chris mới đưa lên, mỗi người trên mạng, ví dụ là Ada, sẽ làm như sau (xem lại [Phần 10](#phần-10-giao-dịch-và-xác-minh-giao-dịch)):

1. Xem lại nội dung các giao dịch đầu vào TXID1 và TXID2. Trong 2 giao dịch này có địa chỉ ví người nhận, đều là PKx. Nên nhớ rằng, các địa chỉ ví này là những chuỗi chữ số vô nghĩa, và không ai biết chúng gắn với ai. Vì vậy, tạm ký hiệu nó là PKx. Ada sẽ tạm ghi nhớ PKx này.
2. Lấy nội dung TXID3, bỏ ra phần chữ ký số của nó, cho chạy qua thuật toán hash, ra được chuỗi hash H1.
3. Bây giờ dùng chìa khóa PKx để giải mã chữ ký số của TXID3 ra được chuỗi hash H2.
4. So sánh H1 và H2. 

Nếu H1 và H2 bằng nhau, nghĩa là giao dịch TXID3 hợp lệ. *Điểm thú vị ở đây là Ada hoàn toàn không biết TXID3 do ai tạo ra*, nhưng cô ấy biết rằng người đó đúng là người đã ký giao dịch TXID3, và người này đúng là người được nhận tiền từ các giao dịch đầu vào TXID1 và TXID2. Như thế là đủ để Ada đồng ý rằng TXID3 là hợp lệ và sẽ đưa nó vào trong block mà cô ấy đang tạo lập.

Như vậy, thay vì sử dụng thông tin định danh, trên mạng lưới Bitcoin, người ta sử dụng PK và SK, trong đó:

- PK, khóa công khai, dùng để nhận tiền, và để xác minh giao dịch.
- SK, khóa riêng tư, dùng để ký xác nhận giao dịch chuyển tiền đi.

Với người sở hữu ví Bitcoin, và không quan tâm đến chi tiết phía sau hệ thống tạo lập và xác minh giao dịch, thì anh ta chỉ cần biết như sau:

- *PK được dùng để nhận tiền*, vì thế, anh ta có thể đưa nó cho bất cứ ai cần chuyển tiền cho anh ta.
- *SK được dùng để tiêu tiền*. Và vi thế, anh ta phải **giữ bí mật** cho riêng mình.

### Chùm chìa khóa và bản chất của ví điện tử

Chris là một anh chàng cẩn thận, và không muốn những kẻ tọc mạch lần ra địa chỉ ví nào đó là của anh ta, trừ người cần chuyển tiền cho anh ta.

Vì vậy, Chris nghĩ ra một cách: cứ mỗi lần một người mới nào đó muốn chuyển tiền cho anh ta, thì anh ta sinh ra một cặp chìa SK - PK, và anh ta chuyển PK mới này cho người đó. Như thế trên blockchain có thể có hàng chục giao dịch chuyển tiền, mỗi trong số chúng lại có địa chỉ ví nhận khác nhau, nhưng thực chất đều là của Chris. Và vì thế, Chris có trong tay cả một chùm chìa khóa.

Nhưng việc quản lý cả chùm chìa khóa như thế thật vất vả. Mỗi cặp chìa lại tương ứng với một khoản tiền riêng biệt (ta nhớ rằng để tiêu tiền gửi đến một PK thì ta cần có SK tương ứng). Riêng việc rà soát để tính tổng số tiền hiện có cũng khiến Chris đau đầu.

Để hỗ trợ người như Chris, đội ngũ phát triển Bitcoin viết ra một phần mềm. Phần mềm này giúp Chris thực hiện tất tần tật những việc liên quan đến quản lý chùm chìa khóa và tiền bitcoin của anh ta, một cách dễ dàng, thuận tiện. Với phần mềm này, Chris có thể:

- Tạo ra các địa chỉ nhận tiền (PK, và kèm theo đó là SK tương ứng).
- Tự tổng hợp số dư dựa trên các giao dịch nhận và gửi tiền liên quan đến Chris.
- Tạo lập các giao dịch chuyển tiền.

Để bảo mật cho dữ liệu chứa trong phần mềm này, Chris mã hóa nó bằng một mật khẩu mà chỉ anh ta biết. Không ai có thể khai thác dữ liệu của Chris mà không giải mã nó bằng mật khẩu này. Điểm độc đáo của phần mềm này, là nó chỉ cần mật khẩu đúng là có thể khôi phục toàn bộ dữ liệu (chùm chìa khóa) cho Chris, mà không cần bất kỳ dữ liệu nào khác. Vì vậy, Chris có thể viết mật khẩu vào một mẩu giấy và cất vào két sắt, yên tâm rằng dù có sự cố khiến tất cả máy tính và điện thoại của anh ta bị mất, thì anh ta chỉ cần cài đặt phần mềm này, cung cấp cho nó mật khẩu viết trên mẩu giấy, thì toàn bộ chùm chìa khóa, cùng với đó là tất cả số bitcoin của anh ta, sẽ được khôi phục và có thể sử dụng ngay lập tức. Trong thực tế, mật khẩu này thường là một tập các từ tiếng Anh có tính dễ nhớ, sắp xếp theo thứ tự, tiện cho ghi chép lại. Người ta gọi chúng là "master password", "master phrases", "recovery phrases", "secret phrases"... ***Trong bất cứ trường hợp nào, hãy luôn giữ chúng thật kỹ cho riêng mình, đừng đánh mất, đừng để lộ cho bất kỳ ai***. Mất mật khẩu ví này, là ta thực sự mất toàn bộ số tiền trong đó, mà **không thể khôi phục** được.

Chính vì vậy, khác với ví thông thường là vật chứa tiền mặt, thì *ví điện tử, hay ví bitcoin, là phần mềm, hay công cụ, dùng để sản sinh, quản lý tập hợp các chìa khóa mã hóa, và cung cấp các tiện ích quản lý tiền số* của một người trên mạng lưới Bitcoin. Khái niệm này cũng đúng với các loại tiền số khác.

Do vậy, khi ta sử dụng ví Bitcoin (hoặc các loại ví tiền số khác), ta có thể thấy mỗi lần ta yêu cầu nó đưa cho ta một địa chỉ để nhận tiền của người khác gửi đến, thì nó có thể đưa ra một địa chỉ khác nhau. Đừng lo, chúng vẫn nằm trong chùm chìa khóa của ví ta. Chúng được sinh ra khác nhau để tăng cường tính vô danh, tránh cho ta nguy cơ bị theo dõi, bị hack. Vì vậy, số tiền chuyển đến chúng, cuối cùng vẫn thuộc sở hữu của ta, và được cộng vào số dư chung của ví.

*Lưu ý rằng những điều nêu ra trong phần này được diễn giải để trở nên dễ hiểu, với mục đích giải thích nguyên lý cơ bản của Bitcoin. Trên thực tế thì phức tạp hơn, ví dụ:*

- *Địa chỉ nhận tiền không đơn giản là PK của người nhận, mà là một chuỗi được mã hóa nhiều bước từ PK đó.*
- *Quy trình xác minh không đơn giản là lấy PK từ giao dịch đầu vào để giải mã chữ ký của người gửi, mà là thực thi một đoạn mã lập trình trước được gắn với giao dịch.*
- *Để đòi hỏi và sử dụng số tiền (UTXO) được gửi cho mình, ta cần phải sử dụng PK của ta để thực thi một đoạn mã lập trình trước được gắn với giao dịch chuyển tiền, gọi là đoạn mã mở khóa (unlock script).*

## Phần 15: Branch, soft fork và hard fork

Ở [Phần 8](#longest-chain), ta đã làm quen với hiện tượng phân nhánh của blockchain, khi một gần như đồng thời có hơn 1 node tìm ra block mới, và gửi các block mới này đến các node còn lại. Trở lại với ví dụ ở Phần 8 (trích dẫn):

> Ví dụ, blockchain hiện là A-B-C-D-E, và trong khi đang tìm nonce cho block mới là F, thì Chris gần như đồng thời nhận được từ Leon và Jill 2 block mới hợp lệ (có nonce khác nhau, nhưng hash tổng vẫn thỏa mãn độ khó) gọi là F1 và F2. Chris sẽ dừng việc tìm F, chấp nhận sử dụng block F1 của Leon như block mới (dù nó chỉ đến trước Jill vài phần trăm giây), và lưu block F2 của Jill lại để dự phòng. Như vậy, trong tay Chris đang có 2 chain sau: "A-B-C-D-E-F1" (chain chính) và "A-B-C-D-E-F2" (chain dự phòng). Gộp lại ta có hình ảnh của một cành cây 2 nhánh, chia tách từ sau block E. Sau đó Chris tiếp tục tìm kiếm block mới (G) trên nhánh Leon. 

Minh họa cho blockchain sau tình huống trên như sau:

```
          F1
         /
A-B-C-D-E
         \
          F2
```

Ở đây ta thấy blockchain từ 1 chuỗi thống nhất đã bị tách ra thành làm đôi, một chuỗi có block cuối là F1, chuỗi kia có block cuối là F2. Ta gọi chuỗi F1 và chuỗi F2 là các nhánh (branch) của blockchain.

Tiếp theo, vẫn trích ví dụ ở Phần 8:

> Tuy nhiên, vì lý do nào đó, Ada lại nhận được F2 của Jill trước F1 của Leon và bắt đầu tìm kiếm block G trên nhánh Jill, ngược lại so với Chris.
>
> Sau một thời gian, Ada là người đầu tiên tìm được block G. Cô ta gửi nó đến toàn bộ mạng lưới. Vì trong một khoảng thời gian đủ dài, chưa có ai tìm được block G ngoài Ada, nên tất cả đều chấp nhận block G do Ada tìm ra. Và vì Ada tìm ra block G trên nhánh Jill, nên giờ đây nhánh của Jill (A-B-C-D-E-F2-G) dài hơn so với nhánh của Leon (A-B-C-D-E-F1). Do đó, Chris buộc phải chuyển từ nhánh anh ta đang làm việc (nhánh Leon) sang nhánh của Jill. Cũng may, là Chris vẫn còn lưu giữ block F2 của Jill làm dự phòng, nên giờ đây anh ta có thể chuyển sang nhánh Jill một cách dễ dàng, và sau đó chỉ việc bổ sung thêm block G của Ada là xong.

Tại thời điểm này, blockchain có hình ảnh như sau:
```
          F1
         /
A-B-C-D-E
         \
          F2-G
```

Như vậy là *chuỗi chính* (*main chain*, tức là *longest chain*) blockchain tiếp tục đi theo nhánh A-B-C-D-E-F2-G. Block F1 lúc này không được sử dụng, vì không nằm trên chuỗi chính, và gọi là uncle block.

Việc hình thành các nhánh như trên diễn ra khá thường xuyên trong quá trình phát triển blockchain, vì đó là điều hết sức bình thường. Thực tế thì quá trình xử lý vấn đề hình thành nhánh và lựa chọn nhánh nào nằm trên chuỗi chính diễn ra rất nhanh, chỉ sau 1 block mà thôi. 

Tuy nhiên, có những trường hợp việc rẽ nhánh này diễn ra lâu hơn (số lượng block trên nhánh nhiều hơn một vài block), thậm chí là vĩnh viễn không hợp nhất lại được. Người ta gọi chúng là các *fork*.

Trong quá trình phát triển blockchain, sẽ có lúc đội ngũ phát triển thấy cần phải thay đổi một số quy tắc của nó, hoặc thực hiện một số sửa đổi trong mã chương trình (để cải tiến, sửa lỗi...). Nếu những sửa đổi này ảnh hưởng đến việc các node xử lý các giao dịch và các block, thì nó có nguy cơ gây ra các fork.

Có 2 loại fork: *hard fork* và *soft fork*. Chúng khác nhau ra sao? Ta sẽ xem xét các ví dụ sau đây.

Giả sử nhóm phát triển Bitcoin, vào một ngày đẹp giời, quyết định rằng cần phải nâng kích thước block từ 1 MByte lên 4 MByte, nhằm tăng tốc độ xử lý giao dịch của toàn hệ thống. Thay đổi này không tương thích với phiên bản hiện có, còn gọi là *không tương thích ngược* (*backward-incompatible*). Họ phát hành phiên bản cập nhật phần mềm dành cho các node để nâng giới hạn này bằng cách thay đổi cấu trúc của block. Tuy nhiên, vì lí do nào đó, không phải tất cả các node đều đồng ý với điều này, nên không phải tất cả các node đều nâng cấp. Sau đó, trên mạng lưới xuất hiện cả các block 1M (truyền thống) và block 4M (loại mới). Những node đã nâng cấp chỉ chấp nhận block 4M, trong khi những node không nâng cấp chỉ chấp nhận block 1M. Vì vậy, blockchain nhanh chóng bị tách ra thành 2 fork, 1 fork vẫn đi theo định dạng block 1M, còn 1 fork thì (kể từ điểm phân tách) chỉ chứa các block 4M. Chúng không bao giờ hợp nhất trở lại, và các node hoạt động duy trì song song cả 2 fork này. Trường hợp này được gọi là *hard fork*.

Bên cạnh đó, cũng có những điều chỉnh trên phần mềm của blockchain mà vẫn duy trì tính *tương thích ngược* (*backward-compatible*) với các node chưa nâng cấp. Nghĩa là những node cũ này vẫn chấp nhận và làm việc được với các giao dịch và block kiểu mới, tuy rằng chúng sẽ không có được những thay đổi do phiên bản nâng cấp mang lại. Tuy nhiên, cần phải đảm bảo rằng số lượng node chấp nhận nâng cấp phải chiếm đa số ngay khi tung ra bản cập nhật. Như thế, sau thời điểm nâng cấp, chỉ có các block theo kiểu mới sẽ được duyệt đưa vào blockchain. Vì thế, sự kiện hard fork sẽ không xảy ra. Và ta gọi cách thức cập nhật điều chỉnh là *soft fork*. Gọi như vậy là để có sự so sánh với hard fork, là  cách thức điều chỉnh gây ra fork mới, chứ soft fork thực sự chẳng hề tạo ra một fork nào. *Để tiến hành một soft fork, cần có được sự đồng thuận của đa số các node trong mạng lưới blockchain*.

Như vậy, có thể nói một cách giản lược như sau:

- *Hard fork là sự kiện gây ra bởi những thay đổi trong phần mềm blockchain, mà không tương thích ngược với phiên bản trước đó, dẫn đến hình thành một nhánh mới hoạt động song song với nhánh chính và không bao giờ nhập lại với nhau.*
- *Soft fork là sự kiện cập nhật phần mềm mà vẫn đảm bảo tương thích ngược với phiên bản trước đó, với số lượng node cập nhật chiếm đa số, và vì thế không tạo ra nhánh mới.*

Ngoài ra, trong thực tế cũng có những dự án sinh ra những blockchain và tiền số mới bằng cách hard fork trên blockchain sẵn có của Bitcoin, như [Bitcoin Cash](https://bitcoincash.org/) (BCH), [Bitcoin Gold](https://bitcoingold.org/) (BTG), [Bitcoin SV](https://bitcoinsv.io/) (BSV).

## Nguồn tham khảo

1. [Bitcoin Project](https://bitcoin.org)
2. [Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf)



