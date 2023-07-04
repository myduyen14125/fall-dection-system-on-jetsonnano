# Config Jetson Nano for Machine Learning

Có rất nhiều bản Jetson Nano khác nhau, bài viết này tương thích với Jetson Nano Developer Kit B01. 
Thời gian để config hoàn thành tốn khoảng từ 2-5 ngày. 

Thiết bị bao gồm:
+ Jetson nano developer Kit B01
+ MicroSD card 32GB/64GB+
+ Nguồn Adapter 5V 4A (20W)
+ Bộ kết nối wifi hoặc module wifi
+ Thiết bị ngoại vi khác: chuột, bàn phím, bàn hình, camera,... hoặc sử dụng SSH (khuyến nghị với máy chạy tốt nếu không sẽ rất lag)

## 1. Flask .img, boot Jetson Nano với microSD

Các Jetpack tương thích chạy được nên Jetson Nano B01 bao gồm từ Jetpack 4.2 -> 4.6. 
Có một bài viết tham khảo khá đầy đủ và chi tiết về cách cấu hình Jetson Nano 
<a href="https://pyimagesearch.com/2020/03/25/how-to-configure-your-nvidia-jetson-nano-for-computer-vision-and-deep-learning/">tại đây</a> 
bởi Pyimagesearch với phiên bản 4.2 (viết vào 2020).
Tuy nhiên, bản 4.2 khá là cũ, mình đã thử nghiệm và nếu mọi người muốn cài đặt TensorFlow 2.x hay các thư viện 
đời mới thì gặp rất nhiều lỗi và không cài đặt được. 
<br>

Mình cài bản Jetpack cao nhất 4.6 có thể tương thích để có thể cài đặt các thư viện học máy trong các bước sau.
Đây là link JetPack SDK 4.6.3: <a href="https://developer.nvidia.com/jetpack-sdk-463">JetPack 4.6.x</a>. 
Sau khi truy cập trang, chọn
<b> Installing JetPack / SD Card Image Method / Jetson Nano Developer Kits </b> => Download the SD Card Image
<br>
Dưới đây là cụ thể từng bước
1. Install balenaEtche - image flashing tool: https://www.balena.io/etcher/
2. Flask vào thẻ nhớ.
   Chú ý thẻ nhớ cần ít nhất 32GB hoặc tốt hơn là 64GB lữu trữ, có thể mua của bất kỳ hãng nào (Kingston, SandDisk,..98MB/s)
4. Boot Jetson Nano với microSD card.
   - Cắm thẻ nhớ đã được boot vào khe cắm jetson nano
   - Cắm điện chờ trong 1 phút (đối với Jetson Nano mới)
   - Đèn xanh sẽ nhấp nháy liên tục tức đã boot thành công
* Sau khi boot thành công, màn hình sẽ hiển thị với Logo của NVIDIA, sau đó sử dụng như hệ điều hành Ubuntu bình thường.
5. Bật terminal và gõ cmd sau để JS chạy với maximun power:
  ``` sudo nvpmodel -m 0 ```
  ``` sudo jetson_clocks ```

## 2. Cài đặt system-level dependencies, python và các thư viện cần thiết
- Xóa libreoffice để tiết kiệm bộ nhớ
  ``` sudo apt-get purge libreoffice* ```
- Clean, remove, update, upgrade
  ``` sudo apt-get update && sudo apt-get clean && sudo apt-get autoremove && sudo apt-get upgrade ```
1. Cài đặt dependencies
  ```
  sudo apt-get install libatlas-base-dev gfortran
  sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev libjpeg8-dev liblapack-dev libblas-dev
  sudo apt-get install nano locate
  ```
  Trên đây là những packages cần thiết cho TensowFlow và một số thư viện học máy khác.
2. Cài python và upgrade pip3
  ```
  sudo apt-get install python3-dev
  sudo apt-get install python3-pip
  sudo pip3 install -U pip testresources setuptools==49.6.0
  ```
3. Cài đặt Python package dependencies
  ```
  sudo pip3 install -U --no-deps numpy==1.19.4 future==0.18.2 mock==3.0.5 keras_preprocessing==1.1.2 keras_applications==1.0.8 gast==0.4.0 protobuf pybind11 cython pkgconfig
  sudo env H5PY_SETUP_REQUIRES=0 pip3 install -U h5py==3.1.0
  ```
4. Cài đặt openCV
   ```
   sudo apt-get install python3-opencv 
   sudo apt-get remove python3-opencv 
   ```



