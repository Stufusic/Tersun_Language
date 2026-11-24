# TERSUN COMPUTING PLATFORM (v<!-- SYNC:START(compiler_version) -->1.0.0<!-- SYNC:END -->)
### *Release v1.0.0 (Kiến Trúc Self-Hosting Zero-C++ Thế Hệ 5) • Poly-Runtime Zones • Universal Runtime (`tersun-rt`) • Balanced Ternary*

[![Self-Hosting](https://img.shields.io/badge/Self--Host-Stage_2_%3D%3D_Stage_3_Zero--C++-brightgreen.svg)](tools/tersunc.stn)
[![CI Pipeline](https://img.shields.io/badge/CI_Pipeline-<!-- SYNC:START(ci_gate_count) -->15<!-- SYNC:END -->_Hard_Gates-brightgreen.svg)](scripts/run_ci.ps1)
[![Poly-Runtime Zones](https://img.shields.io/badge/Poly_Zones-Gate_Z0--Z4_7%2F7_PASS-blue.svg)](Code/src/runtime/README.md)
[![TLLM Native](https://img.shields.io/badge/TLLM_Native-Zero--CRT_|_PE32%2B-blue.svg)](Code/src/tllm/README.md)
[![Package Manager](https://img.shields.io/badge/TPM-Package_Manager_|_Cargo--Style-orange.svg)](bin/tpm.bat)
[![VS Code Extension](https://img.shields.io/badge/VS_Code-<!-- SYNC:START(vscode_ext_version) -->1.0.0<!-- SYNC:END -->-purple.svg)](Code/extension/README.md)
[![Stdlib stdtaf](https://img.shields.io/badge/Stdlib-stdtaf_<!-- SYNC:START(stdtaf_module_count) -->495<!-- SYNC:END -->_modules-teal.svg)](Code/include/stdtaf/README.md)
[![Core Compiler](https://img.shields.io/badge/Version-v<!-- SYNC:START(compiler_version) -->1.0.0<!-- SYNC:END -->--selfhost-blue.svg)](VERSION.md)
[![Academic Curriculum](https://img.shields.io/badge/Curriculum-GT_Vol_1--3_+_LAB-purple.svg)](GT/README.md)
[![License](https://img.shields.io/badge/License-TIPARL_v1.2.0_IP_Protected-red.svg)](LICENSE.md)

> [!NOTE]
> **Single Source of Truth (SSOT)**: Toàn bộ thông số phiên bản và chỉ số đo kiểm trong README này được đồng bộ tự động từ [`VERSION.json`](VERSION.json), [`BENCHMARK_REPORT.md`](BENCHMARK_REPORT.md), [`tools/ci_runner.stn`](tools/ci_runner.stn) và [`Code/include/stdtaf/`](Code/include/stdtaf/README.md) thông qua bộ công cụ Doc-as-Code thuần Tersun (`tools/doc_engine/metrics_sync.stn` & `doc_audit.stn`).

---

## 1. ĐỘT PHÁ CÔNG NGHỆ TRÊN TERSUN v<!-- SYNC:START(compiler_version) -->1.0.0<!-- SYNC:END --> (KEY HIGHLIGHTS)

### 1.0. Trình Biên Dịch Tự Biên Dịch Thuần Tersun Zero-C++ (`tools/tersunc.stn`)
- **Fixed-Point Self-Hosting Thực Thụ (`Stage 2 == Stage 3`)**: [`tools/tersunc.stn`](tools/tersunc.stn) (kết hợp `ModuleBundlerV3`, `TIR v2`, `x64.stn`, `pe_linker.stn`, `aot_rt_core.stn`) biên dịch chính nó trong môi trường sạch `PATH=""` thành PE32+ x64 độc lập (`tersunc_stage2.exe` $\equiv$ `tersunc_stage3.exe`: **`1,012,736` byte**, **`549` hàm sống**, **`0` register spills**, **13 APIs thuộc `KERNEL32.dll`**, SHA-256 `76c42742cd77f5a77406b96468979fa645b189c5ed9c8f298325d5dfa6f811bb`).
- **Tập Tính Năng Native Zero-CRT Hỗ Trợ Trực Tiếp**: `int` / `bool` / `float` / Inline `string` UTF-8 + đường dẫn Win32 UTF-16LE (`CreateFileW`/`ReadFile`/`WriteFile`/`GetCommandLineW`), `struct` (layout + methods), `enum`/`match`, mảng động `[T]` (`push`/`pop`/slice/index), closure có capture, đa file `import` gộp qua `ModuleBundlerV3`, dò `stdtaf/` tương đối (`<exe_dir>/../include/stdtaf` hoặc `TERSUN_STDLIB_DIR`).
- **Chuỗi Công Cụ Native Zero-C++**: `tersunc.exe` (`compile`, `check`, `emit-tir-v2`), `fmt_native.exe`, `pe_iat_audit_native.exe`, và `verify_v5_selfhost_native.exe` đều được chính `tersunc` biên dịch thành PE32+ thuần `KERNEL32.dll`.
- **Phân Định Ranh Giới Trung Thực (Stage 0 vs Native Self-Host)**: Trình host Stage-0 [`setunc.exe`](Code/README.md) (C++20 VM/LSP/DAP/Universal Runtime `tersun-rt`) vẫn phụ trách `Generics <T>`, `dyn Trait`, `async`/`await`, toán tử `?`, LSP/DAP, và các module `@native` (AI BitNet, GPU, Audio, Image, HTTP/GUI). Xem chi tiết tại [`Doc/TERSUN_STDLIB_GUIDE.md`](Doc/TERSUN_STDLIB_GUIDE.md).

### 1.1. Language Server Protocol (LSP 3.17), Time-Travel DAP & VS Code Extension
- **Bảo Vệ Luồng Binary Stdio trên Windows**: Kích hoạt `_setmode(_fileno(...), _O_BINARY)` khi khởi động `setunc lsp`, loại bỏ lỗi vỡ header `Content-Length` do `\r\n`.
- **Bộ Nhớ Đệm AST Kiên Cường (`last_valid_cst`)**: Khi đang gõ dở câu lệnh (ví dụ `user.`), `Parser` ghi nhận lỗi nhưng LSP vẫn giữ bảng ký hiệu gần nhất để trả về gợi ý đầy đủ.
- **Time-Travel Debugger (`setunc dap`)**: Hỗ trợ `stepBack` qua vòng đệm snapshot và tôn trọng chính sách `tersun.zone.toml` (`force_single_core = true` khi debug đa vùng).
- **VS Code Extension**: Manifest đồng bộ với SSOT [`Code/extension/package.json`](Code/extension/package.json) (gói `<!-- SYNC:START(vscode_ext_pkg) -->tersun-1.0.0.vsix<!-- SYNC:END -->`).

### 1.2. Chuẩn Hóa Công Cụ Quản Lý Gói (`tpm`)
- `tpm new <project_name>`: Tạo dự án với `tersun.toml`, `src/main.stn`, `tests/` và `.gitignore`.
- `tpm run [--native]` / `tpm build [--native]`: Tự động biên dịch `.tbc` hoặc `.exe` độc lập.
- `tpm test`: Quét thư mục `tests/`, chạy song song in-memory (zero disk lock collision).
- **Walk-Up Resolver**: Tự động tìm `tersun.toml` khi chạy `tpm` từ bất kỳ thư mục con nào.

### 1.3. Bộ Hạ Bậc Mã Máy Độc Lập TLLM (Zero-CRT Standalone x86-64 / ARM64 / MCU)
- **Zero CRT Invariant**: Sinh file thực thi PE32+ (Windows x64) chỉ từ **4.5 KB – 8.0 KB**, hoàn toàn `0 libc`, `0 MSVCRT`, không cần linker ngoài (`link.exe` hay GCC).
- **An Toàn Ngăn Xếp & Kiểm Tra Biên Không Dấu**: Mảng tĩnh trên stack kèm bẫy kiểm tra biên (`cmp idx, len; jae __tllm_panic_bounds`, mã thoát `101`).
- **Tuân Thủ Win64 ABI & Phân Bổ Thanh Ghi IRC**: Cấp phát 32-byte Shadow Space, căn chỉnh 16-byte và ThinLTO `InlinerPass` tôn trọng ranh giới vùng.

### 1.4. Kiến Trúc Đa Vùng Thực Thi (Poly-Runtime Zones) & Universal Runtime (`tersun-rt`)
- **Tách Biệt Logic & Thực Thi**: File `.stn` mặc định biên dịch theo đường **TLLM Native + GC + 1 Core**; có thể khai báo `system zone(pure | mem=gc|no_gc, exec=1_core|multi_core, group="...", arena_kb=...)` và `@zone_entry` trên từng module (kể cả module `import`).
- **3 Phân Khu Bộ Nhớ Cô Lập & `pure` Zone-Agnostic**:
  1. **Zone 1 (`GC_HEAP`)**: Mark-Sweep và Compacting Sliding GC (**<!-- SYNC:START(compacting_gc_frag) -->0 PPM<!-- SYNC:END -->**).
  2. **Zone 2 (`NeutralPinnedSlabManager`)**: Cầu nối phi khóa chống ABA với trạng thái `OwnedHandle` (move-only) $\to$ `seal_readonly()` $\to$ `SealedHandle` (`retain` đa luồng không cần mutex), sống sót qua 100 chu kỳ Compacting GC.
  3. **Zone 3 (`ThreadLocalFrameArena`)**: Cấp phát O(1) cho vùng `no_gc` (`gc_bytes = 0`, `gc_pauses = 0`).
  4. **Chế độ `pure`**: Tự động suy diễn điểm bất động cho thư viện `Code/include/stdtaf/`, gọi trực tiếp với 0 chi phí cầu nối từ cả `gc` lẫn `no_gc`.
- **An Toàn Biên Dịch Tĩnh & ThinLTO Barrier**: Bắt lỗi `E0920`–`E0922`, phát hiện deadlock đồng bộ xuyên vùng bằng **Tarjan SCC (`E0923`)**, và cấm ThinLTO inline chéo vùng.
- **Đóng Gói `.stnx`/`.stnpkg` & Cache `.tnc` BLAKE3 Pre-RX**: Bảng phân vùng cố định **<!-- SYNC:START(zone_descriptor_bytes) -->40<!-- SYNC:END --> byte**; `tersun-rt.exe` xác thực **BLAKE3 trước khi cấp quyền `VirtualProtect(RX)`** với cắt tỉa LRU trần **<!-- SYNC:START(tnc_lru_cap_mb) -->512<!-- SYNC:END --> MB**.

---

## 2. HƯỚNG DẪN BẮT ĐẦU NHANH (QUICK START)

### Bước 1: Build Toolchain (`setunc.exe`, `tersun-rt.exe`, `setunc_test.exe`)
```powershell
cmake -B Code/build -S Code -G "Ninja"
cmake --build Code/build --target setunc setunc_test tersun-rt -j
```

### Bước 2: Tạo & chạy dự án với TPM
```powershell
bin\tpm.bat new my_first_app
cd my_first_app
..\bin\tpm.bat run
..\bin\tpm.bat test
..\bin\tpm.bat run --native
```

### Bước 3: Cài đặt VS Code Extension
Cài gói extension tương ứng từ VS Code (`Ctrl+Shift+X` $\to$ `Install from VSIX...`, phiên bản `<!-- SYNC:START(vscode_ext_pkg) -->tersun-1.0.0.vsix<!-- SYNC:END -->`, manifest tại [`Code/extension/package.json`](Code/extension/package.json)).

### Bước 4: Biên dịch Native Zero-C++ với `tersunc` & chạy trên `tersun-rt`
```powershell
# 1. Biên dịch trực tiếp bằng trình biên dịch Pure .stn Zero-C++ (sau khi build Stage 2/3)
.\Code\build\tersunc_stage3.exe compile examples\hello.stn -o hello.exe
.\hello.exe

# 2. Hoặc đóng gói .stnx / .stnpkg chạy trên Universal Runtime (tersun-rt)
.\Code\build\setunc.exe pack path\to\app.stn --stnx -o app.stnx
.\Code\build\tersun-rt.exe app.stnx

# 3. Đóng gói workspace đa vùng (.stnpkg)
.\Code\build\setunc.exe pack-workspace GT_LAB\07_poly_zones\ws_demo -o app.stnpkg
.\Code\build\tersun-rt.exe app.stnpkg
```

---

## 3. CÚ PHÁP MẪU CHUẨN TẮC ĐÃ KIỂM CHỨNG

```stn
system zone(pure);

fn ternary_dot_product(weights: [int], inputs: [int]) -> int {
    let mut sum: int = 0;
    let mut i: int = 0;
    while (i < 4) {
        let w = weights[i];
        let x = inputs[i];
        if (w == 1) {
            sum = sum + x;
        } elif (w == -1) {
            sum = sum - x;
        }
        i = i + 1;
    }
    return sum;
}

fn main() -> int {
    let w: [int] = [1, -1, 0, 1];
    let x: [int] = [10, 20, 30, 40];
    println("Ket qua: " + ternary_dot_product(w, x));
    return 0;
}
```

---

## 4. MA TRẬN PHÂN ĐỊNH NĂNG LỰC (CAPABILITY MATRIX)

| Tính Năng / Đường Chạy | `tersunc.exe` (Zero-C++ Native AOT) | `setunc run` (Bytecode VM) | `setunc compile --backend=tllm` | `tersun-rt` (`.stnx` / `.stnpkg`) | Ghi chú & Giới hạn thực tế |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Kiểu dữ liệu cốt lõi** | `int`, `bool`, `float`, Inline `string`, `struct`, `enum`/`match`, `[T]`, closure, multi-file `import` | Đầy đủ (+ `trit`, `tryte`, `taf3`, `Generics <T>`, `dyn Trait`, `async`) | `int` (i64), `.rdata` strings | Hỗ trợ cả đa vùng `gc` & `no_gc` | Kiểm tra biên mảng cứng (Code `101`); AOT dùng stack-slot `[RBP-disp]` |
| **Mô hình Bộ nhớ** | Zero-CRT Win64 PE32+ (`PermHeap` slab 16 MB + `ScratchArena`) | Mark-Sweep / Compacting GC (`<!-- SYNC:START(compacting_gc_frag) -->0 PPM<!-- SYNC:END -->`) | Zero-CRT Stack / Bump Arena | Zone 1 GC + Zone 2 PinnedSlab + Zone 3 Arena | Bảo vệ Pre-RX BLAKE3 `.tnc` cache; `tersunc.exe` chưa có AOT GC |
| **Thư viện chuẩn `stdtaf`** | AOT-safe (`aot_rt_core`, `pe_linker`, `tir_v2`, Win32 UTF-16LE File I/O, `collections`) | <!-- SYNC:START(stdtaf_module_count) -->495<!-- SYNC:END --> module `.stn` ([`stdtaf`](Code/include/stdtaf/README.md)) | Zero-CRT `__tllm_*` helpers | Tự nâng cấp `pure` + `stdtaf/runtime/` (7 module) | <!-- SYNC:START(stdlib_symbol_count) -->70<!-- SYNC:END --> exported symbols được index |
| **GPU CUDA PTX / `@native` AI** | Chưa hỗ trợ trực tiếp | Fallback `CpuSimdBackend` & host `@native` | N/A | Opt-in CMake (`TERSUN_BUILD_EXPERIMENTAL`) | Xem bảng phân loại 495 module tại [`Doc/TERSUN_STDLIB_GUIDE.md`](Doc/TERSUN_STDLIB_GUIDE.md) |

---

## 5. ĐO KIỂM & XÁC MINH TOÀN DIỆN (<!-- SYNC:START(ci_gate_count) -->15<!-- SYNC:END --> HARD CI GATES)

Dự án vận hành quy trình kiểm định hoàn toàn bằng Pure Tersun và CTest/PowerShell:

```powershell
# Chạy trọn bộ <!-- SYNC:START(ci_gate_count) -->15<!-- SYNC:END --> Hard CI Gates (Pure Tersun hoặc PowerShell wrapper)
.\Code\build\setunc.exe run tools\ci_runner.stn
powershell -NoProfile -ExecutionPolicy Bypass -File scripts\run_ci.ps1
```

* **Con số đo thực chứng ([`BENCHMARK_REPORT.md`](BENCHMARK_REPORT.md))**: Semantic Conformance **100.0%** (8/8 bit-exact với C++ & Rust), `A01` đạt **<!-- SYNC:START(aot_alu_us) -->216 us<!-- SYNC:END -->** (`1.00x` C++ `-O3`), Native startup **<!-- SYNC:START(native_startup_ms) -->27.48 ms<!-- SYNC:END -->**, C1M Throughput **<!-- SYNC:START(c1m_throughput) -->22,170,000/s<!-- SYNC:END -->** (`<!-- SYNC:START(c1m_footprint) -->64.2 B<!-- SYNC:END -->`/task, Peak RSS **<!-- SYNC:START(c1m_rss) -->34.5 MB<!-- SYNC:END -->**), Compacting GC **<!-- SYNC:START(compacting_gc_frag) -->0 PPM<!-- SYNC:END -->**.
* **Poly-Runtime Zones (Gate Z0–Z4 & Gate #13)**: `7/7` C++ suites (`TEST-ZONE-1..7`) + [`tests/test_poly_runtime_zones.stn`](tests/test_poly_runtime_zones.stn) + [`GT_LAB/run_lab.stn`](GT_LAB/run_lab.stn) (`Lab 37` + `E0920..E0923`) **PASSED**.
* **Doc-as-Code Tự Chủ**: `version_sync.stn`, `metrics_sync.stn`, `doc_audit.stn --full-links --cap-matrix`, `doc_test.stn`, `doc_seal.stn` **0 violations**.

---

## 6. BẢN ĐỒ TÀI LIỆU & LIÊN KẾT CHÉO TOÀN KHO (CROSS-LINK MAP)

| Phân Hệ | Tài Liệu Chính | Nội Dung Trọng Tâm |
| :--- | :--- | :--- |
| **Lõi Compiler & VM** | [`Code/README.md`](Code/README.md) | Kiến trúc tổng thể C++20, CLI `setunc`, 4 tầng thực thi & hướng dẫn build |
| **Universal Runtime** | [`Code/src/runtime/README.md`](Code/src/runtime/README.md) | `tersun-rt.exe`, `PolyRuntimeLoader`, cache `.tnc` BLAKE3 Pre-RX, Actor/LockFree |
| **Frontend Compiler** | [`Code/src/compiler/README.md`](Code/src/compiler/README.md) | Lexer/Parser, Borrow Checker, Monomorphizer, Poly-Zone Analysis (`E0920`–`E0923`) |
| **Virtual Machine & Bridge** | [`Code/src/vm/README.md`](Code/src/vm/README.md) | NaN-Boxing, Compacting GC 0 PPM, Zone 1/2/3 & `CrossZoneBridgeKernel` |
| **TLLM Native Backend** | [`Code/src/tllm/README.md`](Code/src/tllm/README.md) | Zero-CRT PE32+/ELF64, ThinLTO `InlinerPass` Zone Barrier, `.stnx`/`.stnpkg` |
| **Time-Travel DAP** | [`Code/src/dap/README.md`](Code/src/dap/README.md) | DAP 3.17, `stepBack`, và chính sách debug `tersun.zone.toml` |
| **Tensor & BitNet** | [`Code/src/tensor/README.md`](Code/src/tensor/README.md) | TensorView, BitNet 1.58b AVX2/FMA & EdgeArena |
| **Hardware & Recovery** | [`Code/src/hardware/README.md`](Code/src/hardware/README.md) · [`Code/src/secret/recovery/README.md`](Code/src/secret/recovery/README.md) | Micro-Probe, ARM64/FPGA RTL & Tự phục hồi RL0–RL6 / TQP 2.0 |
| **Stdlib `stdtaf` (<!-- SYNC:START(stdtaf_module_count) -->495<!-- SYNC:END -->)** | [`Code/include/stdtaf/README.md`](Code/include/stdtaf/README.md) · [`Doc/TERSUN_STDLIB_GUIDE.md`](Doc/TERSUN_STDLIB_GUIDE.md) | Thư viện chuẩn thuần Tersun (`495` module), ma trận AOT vs VM & cẩm nang cú pháp |
| **Kiểm thử & Công cụ CI** | [`Code/tests/README.md`](Code/tests/README.md) · [`tests/README.md`](tests/README.md) · [`tools/README.md`](tools/README.md) | Ma trận 13 Hard CI Gates, Gate Z0–Z4 & bộ công cụ Pure Tersun `doc_engine` |
| **Tài liệu & Đặc tả AI** | [`Doc/README.md`](Doc/README.md) · [`Doc/AI_CONTEXT_CHEATSHEET.md`](Doc/AI_CONTEXT_CHEATSHEET.md) · [`Doc/TERSUN_CANONICAL_AI_CODING_SPEC.md`](Doc/TERSUN_CANONICAL_AI_CODING_SPEC.md) · [`Doc/TERSUN_AI_BOOTSTRAP_PROMPT.md`](Doc/TERSUN_AI_BOOTSTRAP_PROMPT.md) | SSOT cho AI Agents, Error Registry, Anti-Hallucination & Honest Gap Matrix |
| **Giáo trình & Lab Thực hành** | [`GT/README.md`](GT/README.md) · [`GT_LAB/PLAN_GT_STN_LABS.md`](GT_LAB/PLAN_GT_STN_LABS.md) | 6 tập Giáo trình Systems & First-Principles (`CLO-1..CLO-37`) & Conformance Labs |

---

## 7. BẢN QUYỀN (LICENSE)
Dự án được bảo hộ theo giấy phép [**TERSUN INTELLECTUAL PROPERTY & ACADEMIC RESEARCH LICENSE (TIPARL v1.2.0)**](LICENSE.md).  
*Bản quyền © 2024–2026 Tác giả Tersun - Stufusic. Bảo lưu mọi quyền.*
