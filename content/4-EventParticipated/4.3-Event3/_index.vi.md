---
title: "Event 3: AWS FCAJ Agent Forge - Deep Dive Day 2"
date: 2026-08-08
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Event 3: AWS FCAJ Agent Forge - Deep Dive Day 2

## Thông tin sự kiện

- **Tên sự kiện:** AWS FIRST CLOUD AI JOURNEY - AGENT FORGE DEEP DIVE
- **Thời gian:** 09:00 AM - 12:00 PM, Thứ Bảy, ngày 08/08/2026
- **Địa điểm:** Tầng 26, Bitexco Financial Tower
- **Diễn giả:** Nghia Tran – Agentic SA; Pham – Cloud Consultant, G-AsiaPacific Vietnam
- **Vai trò:** Người tham dự

## Tổng quan

Agent Forge Deep Dive Day 2 là buổi chuyên sâu về cách xây dựng các hệ thống AI Agent có khả năng đưa vào môi trường production với Amazon Bedrock AgentCore.

Nội dung chương trình được chia thành hai phần. Phần đầu tập trung vào kiến trúc và các thành phần quan trọng của AgentCore, gồm Memory, Evaluations và Observability. Phần sau là Hands-on Lab, nơi người tham gia trực tiếp làm việc với các công cụ trên môi trường AWS.

Cách tổ chức này giúp kết nối phần kiến thức lý thuyết với quá trình triển khai và theo dõi một AI Agent trong thực tế.

## AgentCore Memory

Một trong những nội dung quan trọng nhất của buổi Deep Dive là kiến trúc bộ nhớ của Agent.

AgentCore Memory được tổ chức thành hai nhóm chính là **Short-term Memory (STM)** và **Long-term Memory (LTM)**. Hai nhóm này được kết nối thông qua **Automatic Memory Extraction Module**, giúp hệ thống xử lý và lưu giữ những thông tin phù hợp trong quá trình Agent hoạt động.

### Short-term Memory

**Short-term Memory (STM)** tập trung vào những thông tin cần thiết trong phiên làm việc hiện tại.

STM bao gồm:

- **Chat Messages:** nội dung trao đổi giữa người dùng và Agent.
- **Session State:** trạng thái của phiên tương tác.

Một điểm đáng chú ý của STM là khả năng hỗ trợ **Branching**. Cơ chế này cho phép tạo ra các nhánh hội thoại hoặc luồng xử lý khác nhau mà vẫn giữ được ngữ cảnh của luồng ban đầu.

Branching đặc biệt hữu ích trong những trường hợp người dùng muốn chỉnh sửa một nội dung trước đó hoặc chuyển cuộc hội thoại sang một hướng xử lý khác.

### Long-term Memory

Khác với STM, **Long-term Memory (LTM)** được sử dụng cho những thông tin có giá trị lâu dài và có thể tiếp tục được sử dụng trong những lần tương tác sau.

Một số chiến lược lưu trữ được giới thiệu gồm:

#### Summary

Summary tạo ra các biểu diễn cô đọng từ nội dung và kết quả của quá trình tương tác. Thay vì phải giữ toàn bộ lịch sử hội thoại, Agent có thể sử dụng phần thông tin đã được tổng hợp để duy trì những nội dung quan trọng.

#### User Preferences

User Preferences cho phép hệ thống lưu lại những sở thích hoặc các mẫu hành vi lặp lại của người dùng.

Cơ chế này có ý nghĩa lớn đối với các ứng dụng cần cá nhân hóa. Agent có thể sử dụng những thông tin đã ghi nhận để đưa ra phản hồi phù hợp hơn trong những lần tương tác tiếp theo.

#### Semantic & Episodic Memory

Semantic & Episodic Memory giúp duy trì những kiến thức liên quan đến lĩnh vực cũng như ghi nhận các quyết định hoặc sự kiện đã xảy ra trong quá trình tương tác.

Những thông tin này có thể trở thành dữ liệu tham khảo cho Agent và hỗ trợ cải thiện khả năng xử lý trong những lần sử dụng sau.

## Namespaces và Metadata

Bên cạnh việc phân chia STM và LTM, AgentCore Memory còn sử dụng **Namespaces** và **Metadata** để tổ chức bộ nhớ dài hạn.

### Namespaces

Namespaces được sử dụng để nhóm và cô lập các vùng bộ nhớ theo một cấu trúc logic.

Cấu trúc namespace có thể được tổ chức theo dạng phân cấp và sử dụng các biến định danh như:

- `{actorId}`
- `{strategyId}`

Cách tổ chức này đặc biệt hữu ích khi hệ thống cần quản lý bộ nhớ cho nhiều đối tượng hoặc nhiều chiến lược khác nhau.

### Metadata

Nếu Namespaces giúp xác định và cô lập đối tượng lưu trữ, thì **Metadata** cung cấp phạm vi thông tin chi tiết hơn bên trong namespace.

Các metadata key có thể được lập chỉ mục (**indexed keys**) để hỗ trợ việc lọc dữ liệu trước khi thực hiện truy vấn (**pre-filter**).

Sự kết hợp giữa Namespaces và Metadata giúp việc quản lý bộ nhớ có cấu trúc hơn, đồng thời hỗ trợ kiểm soát phạm vi dữ liệu mà Agent có thể truy xuất.

## Hands-on Lab

Sau phần trình bày về kiến trúc, chương trình chuyển sang phần **Hands-on Lab** dưới sự hướng dẫn của anh Pham.

Người tham dự được trực tiếp thao tác trên môi trường Lab của AWS thay vì chỉ theo dõi phần trình bày.

Các nội dung chính gồm:

- Cấu hình **Add memory** để bổ sung khả năng ghi nhớ và hỗ trợ cá nhân hóa hành vi của AI.
- Sử dụng **AgentCore Evaluations** để theo dõi và đánh giá hiệu suất của Agent.
- Khám phá **Observability** nhằm quan sát luồng xử lý của Agent.
- Làm quen với các công cụ **Harness** trong hệ sinh thái AgentCore.

Phần thực hành giúp mình hình dung rõ hơn cách các thành phần Memory, Evaluations và Observability kết hợp với nhau trong quá trình phát triển một AI Agent.

## Trải nghiệm và kiến thức đạt được

Điểm mình đánh giá cao ở sự kiện là sự kết hợp giữa nội dung chuyên sâu và môi trường thực hành.

Phần trình bày giúp mình hiểu rõ hơn cách thiết kế bộ nhớ cho một AI Agent hiện đại. Việc phân tách **Short-term Memory** và **Long-term Memory** giúp Agent xử lý thông tin theo từng mục đích thay vì phụ thuộc hoàn toàn vào toàn bộ lịch sử hội thoại.

Bên cạnh đó, việc sử dụng **Namespaces** để phân vùng bộ nhớ mang lại một cách tiếp cận rõ ràng hơn trong việc quản lý ngữ cảnh và dữ liệu của Agent.

Phần Hands-on Lab cũng giúp củng cố kiến thức sau khi học lý thuyết. Việc trực tiếp thao tác với Memory, Evaluations và Observability giúp mình hiểu rõ hơn vai trò của từng thành phần trong một hệ thống Agentic production-ready.

## Ứng dụng vào Cloud Finance Platform

Những kiến thức từ AWS FCAJ Agent Forge có thể áp dụng trực tiếp vào định hướng phát triển **Cloud Finance Platform**, đặc biệt là phần trợ lý tài chính sử dụng AI.

### Cá nhân hóa trợ lý tài chính

Chiến lược **User Preferences** của Long-term Memory có thể được sử dụng để trợ lý tài chính ghi nhớ những mẫu hành vi chi tiêu quen thuộc của từng người dùng.

Ví dụ, nếu một người dùng thường xuyên có những nhóm chi tiêu hoặc thói quen tài chính nhất định, Agent có thể ghi nhận các mẫu này và sử dụng chúng trong những lần tương tác tiếp theo.

Điều này giúp chatbot không chỉ trả lời dựa trên câu hỏi hiện tại mà còn có khả năng xây dựng trải nghiệm phù hợp hơn với từng người dùng.

### Phân tách dữ liệu và bảo mật

Cấu trúc **Namespaces** kết hợp với các biến định danh như `{actorId}` có thể được sử dụng để cô lập dữ liệu giữa những người dùng.

Đối với Cloud Finance Platform, điều này đặc biệt quan trọng vì lịch sử giao dịch và ngữ cảnh hội thoại đều chứa thông tin cá nhân.

Việc tổ chức bộ nhớ theo từng phạm vi giúp hạn chế khả năng Agent truy xuất nhầm dữ liệu của người dùng khác và tạo ra một cấu trúc rõ ràng hơn cho việc quản lý dữ liệu.

## Kết luận

AWS FCAJ Agent Forge - Deep Dive Day 2 giúp mình hiểu sâu hơn về cách xây dựng bộ nhớ và quản lý ngữ cảnh cho AI Agent bằng Amazon Bedrock AgentCore.

Ba nhóm kiến thức mình ghi nhận rõ nhất sau sự kiện là **Memory, Evaluations và Observability**. Trong đó, STM, LTM, Namespaces và Metadata cung cấp nền tảng để Agent có thể duy trì thông tin một cách có tổ chức.

Những kiến thức này có thể tiếp tục được áp dụng trong quá trình hoàn thiện Cloud Finance Platform, đặc biệt ở phần trợ lý tài chính cá nhân hóa và quản lý dữ liệu người dùng.

## Hình ảnh sự kiện

![AWS FCAJ Agent Forge - Deep Dive Day 2](https://vvinh118.github.io/fcaj-workshop/4-eventparticipated/4.3-event3/event3.jpg)