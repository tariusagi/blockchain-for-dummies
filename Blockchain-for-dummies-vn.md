# Blockchain & Bitcoin cho phó thường dân

![Bitcoin](assets\bitcoin-2007769_640.jpg)

*[Image by MichaelWuensch from Pixabay](<https://pixabay.com/users/michaelwuensch-4163668/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2007769")*

Nhà bác học Einstein từng nói: *"Nếu anh không thể giải thích vấn đề một cách đơn giản, nghĩa là anh chưa thực sự hiểu nó"*.

Blockchain là một khái niệm không còn mới với dân công nghệ, nhưng với hầu hết mọi người, nó vẫn rất mới và đặc biệt khó hiểu.

Như một nỗ lực trong việc tự đánh giá lại khả năng hiểu biết của bản thân trong quá trình nghiên cứu về blockchain và các ứng dụng của nó, tôi sẽ cố gắng viết lại theo cách *dễ hiểu nhất* có thể, những gì mình thu lượm được về lĩnh vực này. Các bài viết sẽ được đăng thành nhiều phần, song hành với quá trình nghiên cứu của tôi, như một dạng kết quả được đúc rút lại, trong những comment bên trong post này.

Các thông tin tham khảo phần lớn sẽ đến từ đồng tiền số đầu tiên ứng dụng blockchain: [Bitcoin](https://bitcoin.org).

## Phần 1: Blockchain là gì?

Blockchain là chuỗi (*chain*) kết nối các khối (*block*) dữ liệu với nhau theo nguyên tắc: block sau phải chứa *chuỗi hash* của block trước nó, và cứ như thế cho đến tận block đầu tiên (block zero).

Vậy chuỗi hash là gì? Người ta nghĩ ra một thuật toán, mà khi đưa vào đó một khối dữ liệu bất kỳ, sẽ cho ra kết quả là một chuỗi ký tự có độ dài cố định, ngắn hơn rất nhiều so với khối dữ liệu đầu vào. Và quan trọng nhất, đó là chỉ cần một thay đổi nhỏ nhất ở dữ liệu đầu vào, thì chuỗi hash đầu ra sẽ thay đổi hoàn toàn. Không thể có 2 khối dữ liệu đầu vào khác nhau, dù chỉ 1 bit, mà lại sinh ra 2 chuỗi hash giống nhau. Vì thế, chuỗi hash có vai trò như một chữ ký đại diện cho dữ liệu đầu vào.

Phần tiếp theo sẽ giải thích vì sao blockchain yêu cầu mỗi block phải chứa hash của block trước nó.

## Phần 2: Vì sao một block cần chứa hash của block trước nó?

Là để đảm bảo tính toàn vẹn (integrity) về dữ liệu của toàn bộ blockchain.

Khi ta nhận được một blockchain, ta nên kiểm tra xem liệu dữ liệu của nó có bị sai lệch hay không. Trong thực tế có rất nhiều khả năng dẫn đến sai lệch dữ liệu: lỗi đường truyền, lỗi ổ cứng, dính virus, bị cố tình sửa đổi...

Vậy làm thế nào để kiểm tra sự toàn vẹn của blockchain? Rất đơn giản: giả sử blockchain có độ dài N blocks, ta sẽ lấy dữ liệu của block N-1 đưa vào thuật toán hash để tạo ra chuỗi hash của nó, rồi so sánh với giá trị chuỗi hash đang được lưu trữ ở block N. Nếu bằng nhau, nghĩa là blockchain đang OK với 2 block N và N-1. Tiếp tục làm như vậy cho đến block zero. Nếu mọi phép so sánh đều cho kết quả bằng nhau, ta sẽ yên tâm rằng dữ liệu của blockchain này là toàn vẹn. Nếu chỉ cần xuất hiện một kết quả khác nhau, ta sẽ kết luận ngay blockchain này không còn toàn vẹn.

Tuy nhiên thiết kế này chỉ đưa ra cách kiểm tra tính toàn vẹn của blockchain, chứ chưa đảm bảo tính đúng đắn (validity) của nó. Đây là nội dung của phần tiếp theo.

## Phần 3: Tính đúng đắn của blockchain

*Đây là một chủ đề dài, và sẽ cần nhiều phần.*

Một blockchain toàn vẹn không có nghĩa là nó đúng đắn. Một kẻ rành công nghệ có thể tạo ra một blockchain toàn vẹn về dữ liệu, nhưng trong đó chứa đựng những dữ liệu sai khác với thực tế và có lợi cho hắn. Việc này rất dễ dàng: giả sử blockchain hiện có độ dài là 5, gồm các block A-B-C-D-E. Bill, là một kẻ xấu xa, cần sửa đổi dữ liệu ở block C, hắn ta sẽ làm việc đó, rồi tính toán lại hash của block C, đưa hash này vào block D, tiếp tục tính hash của block D, đưa vào block E. Và thế là xong. Hắn đã tạo ra một blockchain toàn vẹn về dữ liệu, nhưng chứa dữ liệu lừa đảo có mục đích, rồi tung ra cho mọi người cùng xem. Như thế, giờ đây tồn tại 2 blockchain, và chúng chỉ giống nhau từ block B về trước, còn từ block C thì khác nhau. Vậy làm thế nào để biết blockchain nào là đúng đắn (valid)?

Có một cách rất dễ dàng: chúng ta bầu ra một người, có tên là Peter, đứng ra xác định blockchain nào là đúng đắn. Peter là một anh chàng đàng hoàng, có uy tín, có tiếng là trung thực, vì thế đa số đều tin vào anh ta. Thế nhưng, nhỡ đâu Peter lại mắc sai sót? Hoặc thậm chí, anh ta thông đồng với Bill, và xác nhận blockchain của Bill là đúng?

Tốt nhất là không dựa vào một cá nhân nào, vì ở thời buổi này, chẳng ai đáng tin cả. Nhưng nếu thế, thì làm thế nào xác nhận tính đúng đắn của một blockchain? Đây là thách thức lớn mang tính quyết định với những người tìm cách ứng dụng blockchain. Giải pháp cho thách thức này được trình bày ở phần tiếp theo.

## Phần 4: Cơ chế đồng thuận

Để xác định một sự việc nào đó đúng hay sai, cơ chế truyền thống sử dụng những cá nhân hoặc tổ chức được bầu chọn hoặc chỉ định, mà ví dụ dễ hiểu nhất là một ông quan tòa. Nhưng đi kèm theo đó là các nguy cơ hiển nhiên: ông quan tòa có năng lực yếu kém, mắc sai sót khi xét xử, bị mua chuộc... và đưa ra phán quyết không công bằng.

Để khắc phục, người ta bổ sung vào đó bồi thẩm đoàn, là những người dân thường được lựa chọn ngẫu nhiên, để theo dõi và đưa ra nhận định về phiên tòa. Quan tòa bắt buộc, theo luật, phải tuân theo kết luận của bồi thẩm đoàn. Thế nhưng, thực tế đầy rẫy ví dụ về việc thành viên bồi thẩm đoàn bị mua chuộc, hoặc mắc sai lầm do định kiến. Có gì lạ đâu, bồi thẩm đoàn chỉ cỡ 10 hay 12 vị mà thôi. Do đó về bản chất, đây vẫn là cơ chế *đồng thuận tập trung* (centralized consensus), chứa đựng đầy rẫy những nguy cơ đưa ra các quyết định không công bằng. Những kẻ xấu: quan tham, trùm mafia, giới chủ độc ác... không thiếu tiền cùng các biện pháp để tấn công, mua chuộc từ bồi thẩm đoàn đến quan tòa.

Tốt nhất, là đưa ra một cơ chế đồng thuận phi tập trung (decentralized consensus), trong đó số lượng thành viên là không dự đoán được (unpredictable), danh tính các thành viên ban bồi thẩm hoàn toàn bí mật, hay là vô danh (anonymous), và vai trò của họ là ngang nhau. Cơ chế này loại bỏ nguy cơ các thành viên bồi thẩm đoàn bị lộ danh tính và bị tấn công hay mua chuộc, và qua đó kỳ vọng rằng các quyết định của bồi thẩm đoàn sẽ là công bằng.

Tuy nhiên, nếu ta chẳng biết được bồi thẩm đoàn gồm những ai, số lượng bao nhiêu, thì làm thế nào ghi nhận được quyết định của họ? Bên cạnh đó, còn cần đảm bảo thông tin về quyết định của bồi thẩm đoàn là đích xác và không bị can thiệp? Nội dung này sẽ được tiếp tục trình bày ở những phần tiếp theo.

## Phần 5: Đồng thuận ngang hàng phi tập trung

Satoshi Nakamoto, một hoặc một nhóm người ẩn danh, đã đưa ra cách giải quyết bài toán đồng thuận phi tập trung trong đặc tả (whitepaper) về Bitcoin. Có thể xem tại [đây](https://bitcoin.org/bitcoin.pdf).

Trở lại với lối diễn giải của chúng ta, thay vì lựa chọn bồi thẩm đoàn trước khi phiên tòa diễn ra, chúng ta mang phiên tòa ra quảng trường và công bố bất kỳ ai nếu muốn cũng có thể tới đó tham dự và đưa ra phán quyết của riêng mình, tức là một phiếu bầu (vote). Mỗi phiếu bầu có vai trò ngang nhau, trên đó không ghi danh tính gì hết (anonymous). Phán quyết cuối cùng sẽ dựa trên cơ chế đa số (majority).

Như vậy, chúng ta chuyển cơ chế đưa ra phán quyết từ chỗ tập trung trong một số nhỏ cá nhân được chỉ định trước, sang cơ chế phi tập trung, tại đó không ai biết trước được sẽ có bao nhiêu người tham gia bầu chọn và cụ thể là những ai. Như thế, kẻ xấu rất khó có thể can thiệp vào kết quả bầu chọn của từng người, dẫn đến khó can thiệp vào phán quyết cuối cùng.

Quay lại với blockchain, khi Bill đưa ra blockchain của hắn, thay vì cử một anh chàng Peter đứng ra đánh giá và xác nhận blockchain của Bill hay một blockchain nào đó là đúng đắn, thì tất cả các blockchain được gửi đến tất cả mọi người: Chris, Leon, Jill, Claire, Ada, Artyom... Mỗi người đều có quyền xem xét và đưa ra bầu chọn của mình. Blockchain nào nhận được nhiều phiếu bầu nhất, sẽ được lựa chọn để tiếp tục sử dụng, các blockchain còn lại sẽ bị tiêu hủy.

Như vậy có vẻ ổn. Thế nhưng nếu Bill phá hoại tiến trình bầu chọn, bằng cách nhanh chóng tạo ra vô số các blockchain khác nhau, hoặc rủ họ hàng hang hốc của hắn tham gia bầu chọn hòng chiếm đa số, thì sao?

Satoshi đã giải quyết khó khăn này bằng cách đưa ra cơ chế *Chứng minh Công việc* (Proof-of-Work, PoW). Cơ chế này được trình bày ở phần tiếp theo.

## Phần 6: Proof-of-Work

Như đã nói cuối phần 5, có 2 khả năng Bill sẽ can thiệp cuộc bầu chọn blockchain, một là nhanh chóng tạo ra vô số các blockchain nhằm làm nhiễu loạn quá trình bầu chọn, hai là rủ anh em nhà hắn tới tham gia bầu chọn hòng chiếm đa số. Thậm chí hắn có thể sử dụng cùng lúc cả 2 cách.

Nhưng nếu ta yêu cầu rằng, mỗi người, để tạo ra một block mới, phải vác đủ 100 viên gạch đến quảng trường trung tâm để sung vào quỹ xây dựng nhà tình nghĩa, thì sao? Để sửa block C, Bill phải vác tới 100 viên, rồi block D, block E nữa, để tạo ra blockchain "đểu" đầu tiên, Bill đã phải vác đến quảng trường tới 300 viên gạch. Chưa kể, hắn không thể cùng lúc vác đến 300 viên. Khỏe mấy, hắn cũng chỉ có thể vác được 50 viên mỗi lần, và phải đi mất đến 1 tiếng đồng hồ từ lò gạch đến quảng trưởng. Để hoàn thành blockchain đểu đầu tiên, tổng cộng hắn mất 300 viên gạch cùng với 6 tiếng đồng hồ. Như vậy đủ khiến Bill phát hoảng khi nghĩ đến việc tiếp tục tạo ra thêm những blockchain đểu khác để làm rối cuộc bình bầu.

Bên cạnh đó, ta cũng yêu cầu rằng, vị nào muốn tham gia bầu chọn, cũng phải làm như Bill. Và ta lại bổ sung thêm rằng, giá trị của một phiếu bầu sẽ được tính trên số lượng gạch mà phiếu đó đại diện. Như thế, Bill có thể rủ thêm anh em hắn đến tham gia, nhưng mỗi người đều phải mất rất nhiều công sức và thời gian để vác đủ số gạch tới quảng trường hòng chiếm đa số. Vì thế, rất ít hoặc thậm chí không ai thèm quan tâm tới đề nghị của Bill. Đơn giản là việc mang được số lượng gạch đủ để chiếm đa số so với cả đám đông ngoài kia, đối với Bill và đồng bọn của hắn, là không thể.

Nói một cách khác, ta bắt mỗi người phải chứng minh rằng anh đã thực sự bỏ công sức ra để xứng đáng giành quyền tạo lập blockchain cũng như bình chọn nó. Giới hạn về khả năng làm việc của anh so với đám đông, chính là giới hạn khả năng phá hoại hoặc can thiệp có chủ đích của anh đến blockchain.

Đó là cách diễn giải đơn giản về cơ chế Proof-of-Work mà Satoshi Nakamoto đã đưa ra để hiện thực hóa đồng tiền số dựa trên blockchain đầu tiên của thế giới: Bitcoin.

Phần tiếp theo sẽ đi sâu hơn vào nội dung kỹ thuật của PoW.

## Phần 7: PoW và độ khó của blockchain

*Phần này có thể bỏ qua nếu bạn không quá quan tâm đến khía cạnh kỹ thuật của cơ chế PoW*

Ngay tại Phần 1, ta đã biết rằng một block cần phải chứa chuỗi hash của block trước nó. Thuật toán hash mà Satoshi đưa ra với Bitcoin là SHA-256, nó tạo ra một chuỗi hash 256 byte từ dữ liệu đầu vào. SHA-256 chạy rất nhanh, một máy tính cá nhân thời nay chỉ mất 1 giây để mã hóa hơn 3 Gigabyte dữ liệu với thuật toán này, trong khi đó kích thước block phiên bản đầu tiên của Bitcoin chỉ là 1 MB. Nghĩa là chỉ mất 0,0003 giây để tính hash của 1 block.

Để tăng khối lượng tính toán khi tạo lập một block, Satoshi yêu cầu mỗi điểm tính toán (node, hay còn gọi là farmer), cần đưa vào block một con số ngẫu nhiên, gọi là nounce, trước khi tính hash cho block đó, và để đủ điều kiện xem xét đưa vào blockchain, hash của block này (gồm cả nounce) phải là một chuỗi bắt đầu bởi N bits có giá trị bằng 0 (zero).

Ta biết rằng chỉ cần dữ liệu đầu vào thay đổi một bit, thì chuỗi hash đầu ra sẽ thay đổi hoàn toàn, và rất ngẫu nhiên. Tuy rằng dữ liệu của block cần tạo lập không thay đổi, nhưng vì có thêm nounce, và với mỗi giá trị khác nhau của nounce, mà hash của block thay đổi rất nhiều.

Do đó, để tìm được một nounce thỏa mãn điều kiện có N zero bits ở đầu chuỗi hash, cần rất nhiều công sức tính toán của máy tính. Cách duy nhất để tìm ra nounce phù hợp là cho nó tăng dần từ 0 cho đến khi hash đầu ra thỏa mãn điều kiện.

Điều kiện nói trên được gọi là độ khó (difficulty) của blockchain. Để được coi là block hợp lệ, giá trị hash của nó phải nhỏ hơn độ khó hiện tại của blockchain. Bên cạnh đó, độ khó này có thể được điều chỉnh tùy vào trạng thái của toàn bộ blockchain, nhằm đảm bảo tính bền vững của nó.

Trên thực tế, sẽ xảy ra trường hợp gần như cùng một thời điểm, có nhiều node cùng tìm ra các nounce thỏa mãn độ khó yêu cầu. Vậy ta sẽ lựa chọn block do node nào giới thiệu?

Nội dung này sẽ được trình bày ở phần tiếp theo.

## Phần 8: Longest chain

Khi một node tạo ra một block hợp lệ, nó sẽ thông báo cho tất cả node khác trong mạng lưới (network) blockchain. Sẽ luôn xảy ra trường hợp gần như cùng một lúc, một node sẽ nhận được những block mới từ những node khác nhau. Khi ấy, nó sẽ chọn block đầu tiên để đưa vào blockchain của mình và tiếp tục làm việc để tạo lập block tiếp theo. Tuy nhiên, các block đến sau vẫn được nó lưu lại để dự phòng. Đến khi block tiếp theo được tạo lập, một trong các nhánh (branch) của blockchain sẽ trở nên dài hơn các nhánh còn lại. Theo nguyên tắc, node này sẽ chấp nhận đi theo nhánh dài nhất (longest branch/chain), tức là có số lượng block hợp lệ lớn nhất, đồng nghĩa với khối lượng công việc đã thực hiện nhiều nhất. Các block thuộc những nhánh còn lại, mặc dù hợp lệ (thỏa mãn độ khó) sẽ bị loại bỏ, và chúng được gọi là block mồ côi (orphan) hoặc block chú (uncle, so sánh với parent block, là block nằm trước trên nhánh chính).

Ví dụ, blockchain hiện là A-B-C-D-E, và trong khi đang tìm nounce cho block mới là F, thì Chris gần như đồng thời nhận được từ Leon và Jill 2 block mới hợp lệ (có nounce khác nhau, nhưng hash tổng vẫn thỏa mãn độ khó) gọi là F1 và F2. Chris sẽ dừng việc tìm F, chấp nhận sử dụng block F1 của Leon như block mới (dù nó chỉ đến trước Jill vài phần trăm giây), và lưu block F2 của Jill lại để dự phòng. Như vậy, trong tay Chris đang có 2 chain sau: "A-B-C-D-E-F1" (chain chính) và "A-B-C-D-E-F2" (chain dự phòng). Gộp lại ta có hình ảnh của một cành cây 2 nhánh, chia tách từ sau block E. Sau đó Chris tiếp tục tìm kiếm block mới (G) trên nhánh Leon.

Tuy nhiên, vì lý do nào đó, Ada lại nhận được F2 của Jill trước F1 của Leon và bắt đầu tìm kiếm block G trên nhánh Jill, ngược lại so với Chris.

Sau một thời gian, Ada là người đầu tiên tìm được block G. Cô ta gửi nó đến toàn bộ mạng lưới. Vì trong một khoảng thời gian đủ dài, chưa có ai tìm được block G ngoài Ada, nên tất cả đều chấp nhận block G do Ada tìm ra. Và vì Ada tìm ra block G trên nhánh Jill, nên giờ đây nhánh của Jill (A-B-C-D-E-F2-G) dài hơn so với nhánh của Leon (A-B-C-D-E-F1). Do đó, Chris buộc phải chuyển từ nhánh anh ta đang làm việc (nhánh Leon) sang nhánh của Jill. Cũng may, là Chris vẫn còn lưu giữ block F2 của Jill làm dự phòng, nên giờ đây anh ta có thể chuyển sang nhánh Jill một cách dễ dàng, và sau đó chỉ việc bổ sung thêm block G của Ada là xong.

Đến đây, ta đã đi qua những phần cơ bản nhất của blockchain. Ở phần tiếp theo, ta sẽ bàn thêm về ý nghĩa các giải pháp mà Satoshi đem lại cho Bitcoin.

## Phần 9: Sổ cái và Bitcoin

Kết hợp thiết kế của blockchain, cơ chế đồng thuận ngang hàng phi tập trung, và cơ chế Proof of Work được trình bày ở các phần trước, mang lại các đặc trưng sau:

- Tính toàn vẹn: dữ liệu trên các block đã có trên blockchain là vĩnh viễn không thể thay đổi và và có thể kiểm tra dễ dàng.
- Tính công khai: bất kỳ ai cũng có thể truy xuất toàn bộ blockchain bất cứ lúc nào.
- Tính đúng đắn: không ai có thể can thiệp thay đổi nội dung blockchain sai với thực tế để làm lợi cho riêng mình.

Với những đặc trưng trên, blockchain rất thích hợp để ứng dụng vào một việc, đó là ghi lại các giao dịch. Nói cách khác, một blockchain chính là một cuốn sổ cái (ledger) tương tự như sổ cái dùng trong công tác kế toán tại các công ty. Chính vì vậy, ứng dụng blockchain mà Satoshi Nakamoto đã đưa ra trong đặc tả của mình chính là một loại tiền số hóa, được đặt tên là Bitcoin. Cái tên này có lẽ là sự kết hợp giữa chữ "bit", là đơn vị dữ liệu nhỏ nhất trong khoa học máy tính, và "coin", tức là đồng xu. Đơn vị tiền tệ biểu diễn giá trị các giao dịch trong "sổ cái" Bitcoin được quy định là "bitcoin", viết tắt là BTC. Ví dụ: trong một block nào đó của blockchain Bitcoin ghi rằng "Chris chuyển cho Leon một giá trị là X", thì ta hiểu rằng "X" ở đây là "X bitcoin" hay "X BTC". Thực tế thì hiện nay, do giá trị của một bitcoin rất lớn (~ 41.000 USD), nên người ta sử dụng "satoshi" (viết tắt "sat") để ghi nhận giá trị các giao dịch bitcoin trong blockchain. 1 satoshi = 0.00000001 BTC (một phần trăm triệu bitcoin).

Điểm khác biệt của "sổ cái" Bitcoin với sổ cái thông  thường đó là tính công khai, một trong 3 đặc trưng, như ta đã nói ở trên. Bất kỳ ai cũng có thể xem toàn bộ lịch sử giao dịch trên Bitcoin. Tuy nhiên, Satoshi đã đưa vào Bitcoin một thiết kế dữ liệu giao dịch, qua đó đem lại cho nó một đặc trưng nữa, đó là tính vô danh, hay nặc danh (anonymity). Trong dữ liệu một giao dịch của Bitcoin, không có danh tính của người gửi và người nhận, mà chỉ có các chuỗi địa chỉ trông có vẻ như là những chuỗi số và chữ cái ngẫu nhiên, và người ta gọi chúng là các địa chỉ ví (wallet address) Bitcoin.

Ví và giao dịch Bitcoin sẽ được làm rõ hơn ở phần tiếp theo.

