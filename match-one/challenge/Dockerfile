# Sử dụng Python 3.11 trên Debian Bookworm (nhẹ hơn và có sẵn Python)
FROM python:3.11-slim-bookworm

# Cập nhật hệ thống và cài đặt các gói cần thiết
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends libmagickwand-dev libmagickcore-dev libzbar-dev && \
    rm -rf /var/lib/apt/lists/*

# Tạo user và group 'ctf' để tránh chạy ứng dụng với root
RUN groupadd -r ctf && useradd -r -g ctf -u 2000 ctf

# Tạo thư mục ứng dụng và gán quyền sở hữu cho user 'ctf'
WORKDIR /app
COPY . /app

# Cài đặt thư viện Python (đảm bảo không phá hủy hệ thống)
RUN pip install --no-cache-dir --break-system-packages -r requirements.txt

# Chỉnh quyền an toàn cho thư mục ứng dụng
RUN chown -R ctf:ctf /app && chmod -R 750 /app

# Expose port 8000
EXPOSE 8000

# Chạy ứng dụng với user 'ctf' để tăng cường bảo mật
USER ctf

# Chạy server
CMD ["python3", "server.py"]
