# Sử dụng Python 3.11 trên Debian Bookworm (nhẹ và có sẵn Python)
FROM python:3.11-slim-bookworm

# Cập nhật hệ thống và cài đặt các gói cần thiết
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends python3-pip python3-dev && \
    rm -rf /var/lib/apt/lists/*

# Tạo user và group 'ctf' để tránh chạy ứng dụng với root
RUN groupadd -r ctf && useradd -r -g ctf -u 2000 ctf

# Thiết lập thư mục làm việc và sao chép mã nguồn ứng dụng
WORKDIR /app
COPY . /app

# Cài đặt thư viện Python mà không lưu cache
RUN pip install --no-cache-dir -r requirements.txt

# Chỉnh quyền an toàn cho thư mục ứng dụng
RUN chown -R ctf:ctf /app && chmod -R 750 /app

# Mở cổng 8000
EXPOSE 8000

# Chạy ứng dụng với user 'ctf' để tăng cường bảo mật
USER ctf

# Cấu hình entrypoint để có thể chạy command tùy chỉnh khi khởi động container
ENTRYPOINT [ "python3" ]

# Chạy server
CMD [ "server.py" ]
