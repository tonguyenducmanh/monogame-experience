# Hướng dẫn Build Shader (FX) MonoGame trên macOS (Chip Apple Silicon M1/M2/M3/M4)

Tài liệu này tổng hợp các bước để thiết lập môi trường Wine và cấu hình hệ thống giúp biên dịch thành công Shader (.fx) trong MonoGame trên các dòng máy Mac sử dụng chip Apple Silicon.

## 1. Cài đặt các công cụ cơ bản

Mở Terminal và cài đặt các trình quản lý gói cần thiết:

```bash
# Cài đặt Homebrew (nếu chưa có)
/bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"

# Cài đặt Wine, Winetricks và 7-Zip
brew install --cask wine-stable
brew install winetricks p7zip
```

## 2. Cài đặt Rosetta 2

MonoGame Shader Compiler (mgfxc) chạy trên kiến trúc x86, do đó bạn cần lớp dịch mã Rosetta:

```bash
softwareupdate --install-rosetta
```

Nhấn A để đồng ý với điều khoản của Apple khi được hỏi.

## 3. Thiết lập môi trường Wine cho MonoGame

Sử dụng script chính thức từ MonoGame để cài đặt .NET Runtime và các thư viện Windows cần thiết vào Wine:

Tạo một file script setup_mgfx.sh:

```bash
curl -sL [https://monogame.net/downloads/net8_mgfxc_wine_setup.sh](https://monogame.net/downloads/net8_mgfxc_wine_setup.sh) > setup_mgfx.sh
chmod +x setup_mgfx.sh
./setup_mgfx.sh
```

Python

# Content for the README.md file

readme_content = """# Hướng dẫn Build Shader (FX) MonoGame trên macOS (Chip Apple Silicon M1/M2/M3/M4)

Tài liệu này tổng hợp các bước để thiết lập môi trường Wine và cấu hình hệ thống giúp biên dịch thành công Shader (.fx) trong MonoGame trên các dòng máy Mac sử dụng chip Apple Silicon.

## 1. Cài đặt các công cụ cơ bản

Mở Terminal và cài đặt các trình quản lý gói cần thiết:

```bash
# Cài đặt Homebrew (nếu chưa có)
/bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"

# Cài đặt Wine, Winetricks và 7-Zip
brew install --cask wine-stable
brew install winetricks p7zip
```

## 2. Cài đặt Rosetta 2

MonoGame Shader Compiler (mgfxc) chạy trên kiến trúc x86, do đó bạn cần lớp dịch mã Rosetta:

```Bash
softwareupdate --install-rosetta
```

Nhấn A để đồng ý với điều khoản của Apple khi được hỏi.

## 3. Thiết lập môi trường Wine cho MonoGame

Sử dụng script chính thức từ MonoGame để cài đặt .NET Runtime và các thư viện Windows cần thiết vào Wine:

Tạo một file script setup_mgfx.sh:

```Bash
curl -sL [https://monogame.net/downloads/net8_mgfxc_wine_setup.sh](https://monogame.net/downloads/net8_mgfxc_wine_setup.sh) > setup_mgfx.sh
chmod +x setup_mgfx.sh
./setup_mgfx.sh
```

Script này sẽ tạo thư mục .winemonogame trong thư mục Home của bạn.

## 4. Cấu hình Biến môi trường (Environment Variables)

Đây là bước quan trọng nhất để VS Code và MGCB Editor có thể build mà không bị lỗi.

Mở file cấu hình shell:

```
nano ~/.zshrc
```

Thêm các dòng sau vào cuối file:

```
# Đường dẫn đến môi trường Wine của MonoGame
export MGFXC_WINE_PATH="$HOME/.winemonogame"

# Tắt Log Vulkan (MoltenVK) để tránh lỗi MSB3073 khi build trong VS Code
export MVK_CONFIG_LOG_LEVEL=1

# (Tùy chọn) Đường dẫn dotnet tools
export PATH="$PATH:$HOME/.dotnet/tools"
```

Lưu (Ctrl+O, Enter) và Thoát (Ctrl+X). Sau đó cập nhật cấu hình:

```bash
source ~/.zshrc
```

