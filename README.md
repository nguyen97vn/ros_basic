1. Tạo một Package
  Sử dụng câu lệnh: catkin_create_pkg tên_package các_gói_phụ_thuộc
    Ví dụ: catkin_create_pkg my_robot std_msgs rospy roscpp tf
    Trong đó, my_robot là tên package chúng ta tạo ra, std_msgs, rospy, roscpp, tf là tên các package phụ thuộc
2. Hiểu về ROS node
  Node có thể được hiểu như một thực thi nhỏ nhất trong hệ thống ROS. Các node có thể giao tiếp được với nhau bằng việc sử dụng topics, services hoặc Parameter Server.
   ROS có các công cụ xử lý các node và cung cấp thông tin cho chúng ta về nó, đó là rosnode. Ví dụ như:
    - rosnode info NODE: hiển thị thông tin về một node.
    - rosnode kill NODE: dừng một node đang chạy hoặc gửi một tín hiệu đựa cung cấp.
    - rosnode list: hiển thị danh sách các node đang chạy.
    - rosnode machine hostname: danh sách các node đang chạy trên một machine đặc biệt hay danh sách các machine.
    - rosnode ping NODE: kiểm tra kết nối giữa các node.
    - rosnode cleanup: làm sạch sự đăng ký thông tin từ các node không thể đạt được.
   Ngoài ra, để thi hành một node, ta sử dụng câu lệnh:
    rosrun tên_package_chứa_node node
    lưu ý: roscore phải được thực thi trước.
3. Hiểu về ROS topic
  Hiểu đơn giản, topic là các chủ đề để cho các node có thể giao tiếp được với nhau. Một node không cần biết nó nhận data từ node nào hoặc truyền cho node nào, mà nó chỉ cần biết là gửi/ nhận data từ/ tới topic đó. Các node có cùng topic thì có thể giao tiếp được với nhau, trao đổi data cho nhau.
   Các công cụ với ROS topic:
    - rostopic bw /topic: Hiển thị dải tần số được sử dụng bởi topic.
    - rostopic echo /topic: In ra các messages tới màn hình.
    - rostopic find message_type: Tìm các topic bằng kiểu tin nhắn của chúng.
    - rostopic info /topic: Xem thông tin về topic đang hoạt động.
    - rostopic pub /topic type args: Truyền data vào topic.
    - rostopic type /topic: in ra kiểu tin nhắn sử dụng của topic.
 
4. Hiểu về ROS services và Parameters
Service:
  Khi chúng ta cần một kiểu giao tiếp yêu cầu / hồi đáp trong ROS, chúng ta phải sử dụng ROS services. Nó được định nghĩa bằng việc sử dụng một cặp messages. Chúng ta phải định nghĩa một kiểu dữ liệu cho yêu cầu và phản hồi trong file srv. Nó được chứa trong thư mục srv.
  Trong ROS services, một node hoạt động như là một ROS server nơi mà service khách có thể yêu cầu từ server, nếu server hoàn thành một lộ trình dịch vụ, nó sẽ gửi kết quả tới service khách.
  Có 2 công cụ để lấy thông tin tử ROS service, thứ nhất là rossrv, cái này tương tự như rosmsg. Thứ hai là rosservice:
    - rosservice call /service args: gọi service bằng việc sử dụng các argumetn được đưa.
    - rosservice find service_type: tìm các services trong kiểu service được đưa.
    - rosservice info /services: hiển thị thông tin về service.
    - rosservice type /service: hiển thị kiểu service của một service được đưa
    - rosservice uri /service: hiển thị service ROSRPC URI.
    
Parameter:
  Trong khi chúng ta viết chương trình cho một robot, chúng ta sẽ phải định nghĩa các tham số robot như là các hệ số P, I, D. Khi số lượng tham số nhiều, chúng ta nên lưu trữ nó trong một file trong trường hợp những tham số đó được sử dụng trong nhiều chương trình. ROS cung cấp một server tham số, cái mà là một server nơi mà tất cả các nodes có thể truy cập các tham số từ server này. Một node có thể đọc, viết, chỉnh sửa và xóa giá trị tham số từ tham số server.
  Chúng ta có thể lưu trữ tham số theo các kiểu dữ liệu khác nhau:
    32-bit integers
    booleans
    strings
    doubles
    iso8601 dates
    list
    base64-encoded binary data
