# rongmalisheng.github.io
"""皮卡丘抛硬币 - HTTP 服务器
运行后在同一WiFi下的手机浏览器访问显示的地址即可打开。
"""
import http.server
import socket
import os
import sys

PORT = 8080

# 切换到脚本所在目录
os.chdir(os.path.dirname(os.path.abspath(__file__)))

# 获取本机局域网IP
def get_local_ip():
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        s.connect(("8.8.8.8", 80))
        ip = s.getsockname()[0]
        s.close()
        return ip
    except:
        return "127.0.0.1"

local_ip = get_local_ip()

class Handler(http.server.SimpleHTTPRequestHandler):
    def log_message(self, format, *args):
        print(f"[访问] {args[0]}")

print("=" * 50)
print("  ⚡ 皮卡丘抛硬币 - 服务器已启动 ⚡")
print("=" * 50)
print(f"  电脑打开: http://localhost:{PORT}")
print(f"  手机打开: http://{local_ip}:{PORT}")
print()
print("  确保手机和电脑连接在同一个WiFi网络")
print("  按 Ctrl+C 停止服务器")
print("=" * 50)

try:
    http.server.HTTPServer(("0.0.0.0", PORT), Handler).serve_forever()
except KeyboardInterrupt:
    print("\n服务器已停止")
    sys.exit(0)
