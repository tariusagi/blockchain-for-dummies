# Blockchain & Bitcoin cho phó thường dân

![Bitcoin](assets/title-vn.jpg)

*[Image by MichaelWuensch from Pixabay](https://pixabay.com/users/michaelwuensch-4163668/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2007769)*

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

Với những đặc trưng trên, blockchain rất thích hợp để ứng dụng vào một việc, đó là ghi lại các giao dịch. Nói cách khác, một blockchain chính là một cuốn sổ cái (ledger) tương tự như sổ cái dùng trong công tác kế toán tại các công ty. Chính vì vậy, ứng dụng blockchain mà Satoshi Nakamoto đã đưa ra trong đặc tả của mình chính là một loại tiền số hóa, được đặt tên là Bitcoin. Cái tên này có lẽ là sự kết hợp giữa chữ "bit", là đơn vị dữ liệu nhỏ nhất trong khoa học máy tính, và "coin", tức là đồng xu. Đơn vị tiền tệ biểu diễn giá trị các giao dịch trong "sổ cái" Bitcoin được quy định là "bitcoin", viết tắt là BTC. Ví dụ: trong một block nào đó của blockchain Bitcoin ghi rằng "Chris chuyển cho Leon một giá trị là X", thì ta hiểu rằng "X" ở đây là "X bitcoin" hay "X BTC". Thực tế thì hiện nay, do giá trị của một bitcoin rất lớn (~ 41.000 USD), nên người ta sử dụng "satoshi" (viết tắt "sat") để ghi nhận giá trị các giao dịch bitcoin trong blockchain. 1 satoshi = 0,00000001 BTC (một phần trăm triệu bitcoin).

Điểm khác biệt của "sổ cái" Bitcoin với sổ cái thông  thường đó là tính công khai, một trong 3 đặc trưng, như ta đã nói ở trên. Bất kỳ ai cũng có thể xem toàn bộ lịch sử giao dịch trên Bitcoin. Tuy nhiên, Satoshi đã đưa vào Bitcoin một thiết kế dữ liệu giao dịch, qua đó đem lại cho nó một đặc trưng nữa, đó là tính vô danh, hay nặc danh (anonymity). Trong dữ liệu một giao dịch của Bitcoin, không có danh tính của người gửi và người nhận, mà chỉ có các chuỗi địa chỉ trông có vẻ như là những chuỗi số và chữ cái ngẫu nhiên, và người ta gọi chúng là các địa chỉ ví (wallet address) Bitcoin.

Ví và giao dịch Bitcoin sẽ được làm rõ hơn ở các phần tiếp theo.

## Phần 10: Giao dịch và xác minh giao dịch

*Đây là một trong những phần có thể nói là khó hiểu và quan trọng nhất khi tìm hiểu cách thức hoạt động của Bitcoin.*

Trước hết, cần phải hiểu cách mà Bitcoin xác minh và thực hiện các giao dịch gửi tiền (bitcoin) đến cho ta cũng như các giao dịch mà ta chuyển tiền cho người khác.

Giả sử Chris cần chuyển cho Leon 50 BTC và cho Jill 40 BTC. Anh ta sẽ nói với mọi người thế nào? Có phải là: *"Này mọi người, tôi sẽ chuyển 50 cho Leon, và 40 cho Jill"*? OK được thôi. Vấn đề là, **Chris có đủ tiền để chuyển đi số tiền trên hay không**?

Thông thường, khi có phát sinh giao dịch gửi hay nhận tiền, các hệ thống kế toán sẽ ghi nhận giao dịch, tính toán số dư (balance), rồi lưu số dư này lại để tính toán cho các giao dịch tiếp theo. Không nhất thiết phải tính toán và ghi nhận số dư sau mỗi giao dịch, nhưng thường việc này sẽ được thực hiện theo kỳ, ví dụ cuối ngày hay cuối tháng. Lý do của cách làm này, là để tăng tốc độ xử lý giao dịch. Thay vì phải cộng trừ tất cả các giao dịch từ đầu của cả hệ thống cho đến trước giao dịch cần thực hiện, để xem số dư còn đáp ứng hay không, thì hệ thống chỉ cần làm thế với các giao dịch từ đầu kỳ. Dù sao, tính toán số lượng giao dịch của một vài ngày vẫn nhanh hơn là vài năm, phải không?

Tuy nhiên, phương pháp trên tiềm ẩn rủi ro rất lớn. Chris có thể sinh ra tham lam, và tìm cách sửa số dư đầu kỳ của anh ta để có nhiều tiền hơn. Vì hệ thống chỉ xác minh giao dịch dựa trên số dư đầu kỳ, nên Chris chỉ cần can thiệp vào con số này và một số lượng nhỏ giao dịch trước đó trong kỳ. Như thế rõ ràng là đỡ tốn công sức hơn là phải chỉnh sửa toàn bộ các giao dịch từ đầu hệ thống.

Với tầm nhìn về một hệ thống xử lý giao dịch công khai theo mô hình mạng phân tán ngang hàng có quy mô toàn cầu, Bitcoin cần phải được thiết kế sao cho rủi ro bị tấn công, sửa đổi là thấp nhất. **Vì thế, trong Bitcoin, chẳng có cái gì gọi là số dư cả**.

Vậy nếu Chris muốn chuyển 50 BTC cho Leon và 40 BTC cho Jill, thì anh ta làm thế nào để thuyết phục mọi người là anh ta có đủ ít nhất 90 BTC để thực hiện 2 giao dịch trên? Vì nếu anh ta không chứng minh được rằng anh ta đang có ít nhất 90 BTC trong tay, thì mạng lưới Bitcoin, tức là những người khác: Leon, Jill, Ada, Claire, Artyom..., sẽ không chấp nhận 2 giao dịch mà anh ta đang muốn tiến hành.

*Trong Bitcoin blockchain, mọi giao dịch đều được định danh bởi một chuỗi mã số, gọi là mã số định danh giao dịch (Transaction's Identification - TxID). Ta sẽ nói một cách ngắn gọn là mã giao dịch. Khi một giao dịch được chấp nhận vào ghi vào blockchain, thì cả dữ liệu của giao dịch lẫn mã giao dịch của nó đều được lưu giữ.*

Và đây là cách mà Chris làm để thuyết phục mọi người rằng anh ta có đủ tiền để thực hiện 2 giao dịch mong muốn. Anh ta cung cấp cho mọi người một danh sách các mã số giao dịch trước đó (đã được ghi trên blockchain), trong đó Chris là người được nhận tiền. Ví dụ, Chris bảo: *"Này mọi người, trước đây Ada và Artyom đã chuyển cho tôi một số tiền, mã giao dịch của chúng là TxID1 và TxID2, và bây giờ, tôi sẽ chuyển cho Leon 50 BTC, và chuyển cho Jill 40 BTC"*. Những giao dịch mà Chris liệt kê trong đó anh ta là người nhận tiền, được gọi là các giao dịch đầu vào (*input transaction*s), ở đây là *TxID1* và *TxID2*. Mọi người sẽ rà soát trên blockchain để tìm kiếm 2 giao dịch có mã số *TxID1* và *TxID2*, sau đó kiểm tra nội dung các giao dịch này, mục đích là để trả lời các câu hỏi sau:

1. Các giao dịch đầu vào này có tồn tại trên blockchain không?
2. Các giao dịch trên có đúng là chuyển tiền cho Chris không?
3. Số tiền của mỗi giao dịch trên là bao nhiêu?
4. Tổng số tiền Chris nhận được từ các giao dịch trên có đủ để anh ta thực hiện các giao dịch chuyển tiền đi hay không?

Nếu tất cả các câu trả lời là đúng, thì giao dịch của Chris sẽ được *chấp nhận* (verified) và sẽ được ghi vào blockchain.

Ở đây ta thấy rằng để kiểm tra một giao dịch mới, mọi người phải rà soát toàn bộ các transactions trong cả blockchain. Tại thời điểm viết bài này, tổng số giao dịch của Bitcoin đã lên tới gần 680 triệu, và trung bình có tới hơn 260 nghìn giao dịch mới mỗi ngày. Như vậy, việc xác minh giao dịch hẳn nhiên phải trở nên rất chậm chạp và hạn chế khả năng mở rộng của Bitcoin. 

Phải có cách nào đó tốt hơn để khắc phục vấn đề này. Giải pháp đó sẽ được trình bày ở phần tiếp theo.

## Phần 11: UTXO

Ở cuối Phần 10, ta đã đặt ra vấn đề làm thế nào để giảm tải cho việc xác minh các giao dịch, khi mỗi người đều phải rà soát gần như toàn bộ các giao dịch đã có trên blockchain để xác minh một giao dịch mới.

Trở lại với ví dụ của chúng ta. Mọi người đều đã xác nhận giao dịch của Chris là OK và giao dịch này sẽ được ghi vào blockchain. Ta đã biết rằng giao dịch này liệt kê 2 giao dịch đầu vào là TxID1 và TxID2, và ta đặt cho giao dịch mới được ghi nhận của Chris là TxID3. Tại thời điểm này, rõ ràng là vai trò cung cấp dòng tiền vào của TxID1 và TxID2 đã hết, vì toàn bộ số BTC của 2 giao dịch này đã đi vào giao dịch TxID3 do Chris mới tạo ra. Với Bitcoin, chúng được coi là những *"giao dịch đã được sử dụng"* (*spent transaction*). Theo nguyên tắc của Bitcoin, một giao dịch chỉ có thể được sử dụng một lần duy nhất. Trong trường hợp khi TxID3 của Chris được chấp thuận, thì TxID1 và TxID2 đều đã được sử dụng, và không giao dịch nào khác được sử dụng chúng làm giao dịch đầu vào nữa. Và vì thế, không ai còn quan tâm đến 2 giao dịch này nữa. Tất cả sẽ bỏ qua 2 giao dịch có mã số TxID1 và TxID2 trong khi rà soát trên blockchain. Bằng cách đó, Bitcoin giảm đáng kể số lượng giao dịch cần rà soát khi xác minh một giao dịch mới.

Nhưng việc cải tiến chưa dừng lại ở đó!

Ở trên, ta biết rằng TxID1 và TxID2 đã được sử dụng, và chẳng ai cần đến chúng nữa trong quá trình xác minh giao dịch đầu vào. Tiếp tục với ví dụ của chúng ta: TxID3 là mã giao dịch của Chris, trong đó TxID1 và TxID2 là 2 giao dịch đầu vào, cung cấp dòng tiền vào cho Chris để anh ta yêu cầu 2 giao dịch mới để chuyển tiền cho Leon và Jill. Hãy gọi 2 giao dịch con này là TxID4 và TxID5. Tại thời điểm TxID3 được ghi nhận vào blockchain, TxID4 chứa 50 BTC, còn TxID5 chứa 40 BTC. Số tiền này đều chưa được ai sử dụng. Chúng được gọi là *"số tiền đầu ra chưa được sử dụng"* (Unspent Transaction Ouput - UTXO). Thuật ngữ này rất khó dịch cho thoát, nên từ giờ ta sẽ gọi chúng là UTXO. Chỉ các UTXO mới được sử dụng để làm đầu vào cho các giao dịch. Điều này rất dễ hiểu: anh chỉ có thể sử dụng số tiền anh chưa sử dụng mà thôi.

UTXO có vai trò vô cùng quan trọng trong thiết kế của Bitcoin. Mỗi node trong mạng lưới Bitcoin đều có một bảng theo dõi các UTXO này (được gọi là tập hợp UTXO, *UTXO set*) và cập nhật nó sau mỗi giao dịch. Thay vì phải rà soát trên blockchain để xác minh các giao dịch, các node chỉ cần rà soát trên UTXO set, sẽ nhanh hơn rất nhiều. Một phần vì kích thước dữ liệu của UTXO nhỏ hơn và đơn giản hơn block, một phần vì số lượng các UTXO có thể giảm đi sau một giao dịch. Đó là trường hợp số UTXO được sử dụng để cung cấp dòng tiền vào của một giao dịch lớn hơn số UTXO phát sinh sau giao dịch. Giả sử trong TxID3, Chris chỉ chuyển tiền cho Leon, mà không chuyển cho Jill, như thế sau khi giao dịch được thực hiện, 2 UTXO của TxID1 và TxID2 đã được tiêu thụ, và chỉ phát sinh 1 UTXO mới mà thôi. Do vậy, số lượng UTXO cần theo dõi trong UTXO set đã giảm đi 1. Trong khi với thời gian, kích thước blockchain chỉ có tăng chứ không giảm, thì kích thước UTXO set có thể dao động quanh một khoảng nhỏ hơn nhiều. Trong khi hiện nay tổng kích thước blockchain của Bitcoin đã lên tới hơn 350 Gigabyte, thì kích thước trung bình của UTXO set chỉ khoảng 3.5 Gigabyte, hoàn toàn đủ nhỏ để chứa hẳn trong bộ nhớ máy tính, qua đó tăng đáng kể tốc độ xác minh giao dịch của node.

***Lưu ý:***

- *Việc lưu trữ, quản lý UTXO set này là việc riêng của mỗi node. UTXO set không được lưu trên blockchain.*
- *Thực tế cấu trúc dữ liệu cũng như cách thức xử lý các giao dịch và UTXO của Bitcoin phức tạp hơn rất nhiều. Tuy nhiên mục tiêu của bài này không phải để đi sâu vào các chi tiết đó.*

## Phần 12: Tiền thừa, phí giao dịch và coinbase

Quay trở lại ví dụ giao dịch của Chris, ta để ý rằng 2 UTXO đầu vào cung cấp cho nó 100 BTC (50 từ Ada và 50 từ Artyom), nhưng đầu ra chỉ có 90 BTC mà thôi (50 cho Leon, 40 cho Jill). Vậy còn 10 BTC thừa ra (change) thì xử lý ra sao?

Bitcoin không tự động ghi nhận 10 BTC tiền thừa này lại cho Chris. Ta nhớ ở Phần 10 đã nói rằng Bitcoin không có khái niệm số dư. Mọi con số trên Bitcoin đều phải tính toán từ các giao dich và các UTXO. Nếu vậy, Chris sẽ bị mất toi 10 BTC hay sao?

Dĩ nhiên Chris không muốn thế. Cho nên anh ta bổ sung thêm 1 nội dung nữa trong giao dịch của mình, đó là chuyển 10 BTC ngược trở lại cho mình. Như thế, sau khi thực hiện giao dịch TxID3, ta có 3 UTXO mới như sau:

1. 50 BTC cho Leon.
2. 40 BTC cho Jill.
3. 10 BTC cho chính Chris.

Việc chuyển lại tiền cho chính mình nghe rất khôi hài với hầu hết mọi người, nhưng nó rất có lý với Bitcoin. Bởi vì Bitcoin không phải đẻ thêm ra một cơ chế khác để quản lý số dư, mà lý do thì ta đã biết: số dư là một điểm rủi ro về an ninh, rất dễ bị tấn công khai thác.

Trở lại với Chris. Trong lúc lập giao dịch, anh ta nghĩ rằng, có lẽ nên khuyến khích mọi người tham gia vào xử lý giao dịch của anh ta. Như thế mọi người sẽ nỗ lực hơn và vì thế giao dịch của anh ta sẽ được thực hiện nhanh hơn. Chris đang rất vội! Nhưng khích lệ mọi người bằng cách nào? Thôi thì để lại 1 BTC cho bất cứ ai đưa được giao dịch này vào blockchain. Vì thế, Chris điều chỉnh giao dịch chuyển tiền như sau:

1. 50 BTC cho Leon.
2. 40 BTC cho Jill.
3. 9 BTC cho chính Chris.

Như thế, còn thừa ra 1 BTC. Bitcoin có quy định rằng, nếu sau một giao dịch mà có một lượng tiền thừa, không thuộc vào một UTXO nào, thì nó sẽ chuyển số tiền thừa đó cho người nào có công đưa được giao dịch đó vào blockchain (tức là người tạo ra được block mới, trong đó chứa giao dịch này, và block đó được ghi nhận vào blockchain). Khoản tiền này được gọi là *phí giao dịch* (*transaction fee*).

Khoản phí này được chuyển đến người có công tạo block thế nào? Bitcoin cho phép người tạo block đưa vào đầu danh sách của giao dịch của block một giao dịch đặc biệt, được gọi là *coinbase* transaction. Người được nhận tiền từ giao dịch coinbase chính là người tạo block, còn giá trị là tổng số tiền phí giao dịch từ tất cả các giao dịch trong block, cùng với 1 khoản thưởng đặc biệt, gọi là *block reward*. Ta sẽ bàn về block reward ở phần sau. Như vậy, nếu may mắn đến với Ada, và block của cô ấy được chấp nhận, thì Ada sẽ có thêm được một UTXO với số tiền ghi trong coinbase của block.

Phần tiếp theo sẽ bàn về block reward và cơ chế đào (mining) bitcoin.
