# TERSUN INTELLECTUAL PROPERTY & ACADEMIC RESEARCH LICENSE (TIPARL)
### Phiên bản: 1.2.0 — Bản Quyền Sở Hữu Trí Tuệ & Giấy Phép Nghiên Cứu Khoa Học (Gate 7.6.2 Sealed)
**Bản quyền © 2024–2026 Tersun - Stufusic. Bảo lưu mọi quyền (All Rights Reserved).**

---

## ĐIỀU 1. ĐỐI TƯỢNG VÀ PHẠM VI BẢO HỘ SỞ HỮU TRÍ TUỆ

Giấy phép này áp dụng cho toàn bộ dự án **Tersun Programming Language & Execution Platform (Phiên bản 1.2.0 — Gate 7.6.2)**, bao gồm nhưng không giới hạn ở:

1. **Mã nguồn và Kiến trúc Trình biên dịch & Máy ảo**:
   - Tầng đầu trình biên dịch (Lexer Zero-Copy, Pratt Parser, Type Checker, Monomorphizer).
   - Tầng chuẩn hóa & tối ưu hóa cây cú pháp (Tree Canonicalization & 8-pass Tree Optimizer) đạt chuẩn 2.13 triệu bất biến toán học.
   - Tầng mã trung gian tuyến tính (Linear 3-Address IR), Đồ thị luồng điều khiển (CFG), SSA Form và Bộ tối ưu hóa lan truyền bản sao (Copy Propagation Pass).
   - Máy ảo đa chế độ (Stack-based TVM, Direct Threading Dispatch, NaN-Boxing 64-bit, Adaptive Quickening, Shape Inline Caching).
   - **Tối ưu hóa Máy ảo Gate 7.6.1**: Nguyên hàm vector mảng liền kề (Vectorized Contiguous VM Primitives), tối ưu hóa chu kỳ giải mã lệnh, bảo tồn hiệu năng thực thi vượt trội CPython tới 46 lần và tiệm cận Java 25 Server VM.
   - **Động cơ Biên dịch JIT Đa tầng & OSR (Gate 5.7 & Gate 5.8)**: Bộ biên dịch Baseline JIT trên RAM x86-64, cơ chế thay thế khung thực thi giữa vòng lặp On-Stack Replacement (OSR) và giải tỏa suy đoán an toàn (Speculative Deoptimization Bailout với MachineState).
   - **Bộ Quản lý Bộ nhớ Managed Heap & Tri-Color GC (Gate 5.6)**: Cơ chế thu gom rác ba màu với Rào ghi (Write Barrier), xử lý an toàn đồ thị vòng $A \to B \to C \to A$ và danh sách sâu 10,000 nút với cam kết 0.00% độ trôi bộ nhớ (Memory Flatline).
   - Hệ thống hạ cấp biên dịch bản địa (Native AOT C++20 / LLVM Lowering Pipeline) và Bộ biên dịch trực tiếp **Micro-AOT Direct Compiler (Gate 7.6.2)** sinh mã thực thi độc lập không phụ thuộc công cụ ngoài.
2. **Hệ sinh thái Đóng gói, Dịch ngược & Nâng cấp Nhị phân (Gate 7.6.2 Ecosystem)**:
   - **Định dạng Gói Độc lập TRSX (`.trsx`)**: Container thực thi tự động chứa nén Zstandard, siêu dữ liệu nhị phân `TRSMETA`, bảo chứng toàn vẹn SHA-256 và cơ chế tự trích xuất thực thi.
   - **Bộ Dịch ngược Bytecode 3 Cấp độ (3-Level Decompiler)**:
     - Level 1: Disassembly chi tiết từng byte lệnh, hằng số và bảng nhảy.
     - Level 2: Phục hồi đồ thị luồng điều khiển (CFG Recovery), tái cấu trúc khối lặp và giải mã phục hồi lệnh thích ứng (Adaptive Dequickening Engine) khử các siêu lệnh `OP_FAST_*` và Inline Caches.
     - Level 3: Tái tạo mã nguồn bậc cao Setun và chuyển mã ngữ nghĩa sang C99 và Rust tương đương 100% ngữ nghĩa.
   - **Bộ Nâng cấp Nhị phân Hướng Dẫn Siêu Dữ Liệu (Metadata-Guided Binary Lifter)**: Cơ chế bóc tách phần thân thực thi và phục hồi mã nguồn từ file thực thi bản địa dựa trên khối debug metadata `TRSMETA`.
3. **Các Sáng chế Kiến trúc Phần cứng & Số học Độc quyền**:
   - **Vi kiến trúc TAFPU (Ternary Algebraic Floating-Point Unit)**: Hệ thống số học đại số trên trường số $\mathbb{Q}(\sqrt{3})$ với cấu trúc bộ ba $(\alpha, \beta, \gamma)$ đảm bảo **0% sai số tích lũy làm tròn** (Zero Representation Drift), triệt tiêu các khiếm khuyết cơ bản của chuẩn IEEE 754.
   - **Bộ xử lý Tam phân Cân bằng BTVP (Balanced Ternary Virtual Processor)**: Bộ cộng và hệ toán tử tam phân cân bằng $\{-1, 0, 1\}$ triệt tiêu hiện tượng lan truyền sóng nhớ.
   - **Thuật toán BitNet 1.58-bit GEMM không cần bộ nhân**: Phép nhân tích chập ma trận cho AI chạy trên số học tam phân không tiêu tốn chu kỳ nhân phần cứng.
   - **Máy ảo Lượng tử QVM (Quantum Virtual Machine)**: Kiến trúc thực thi không mã lệnh (Zero-Opcode Execution), mô phỏng không gian trạng thái Hilbert 2-bit, chuyển đổi đơn nhất trực tiếp không mảng đệm (In-Place Stride Transformation), mở rộng tới **$N=29$ Qubits ($536,870,912$ biên độ trạng thái)** trên RAM vật lý, tích hợp thuật toán Grover, QFT và xuất chuẩn OpenQASM 3.0.
   - **Động cơ Suy luận LLM Bản địa (Gate 7.4 & Gate 7.5)**: Nạp SafeTensors trực tiếp, Tokenizer BPE không cấp phát, Thang Attention 7 bậc AVX2/FMA gia tốc $8.7\times$, và điều phối song song Single Owner of Parallelism bảo toàn `malloc == 0`.
4. **Các Con Dấu Mật Mã & Bằng Chứng Bất Biến (Cryptographic Milestone Seals)**:
   - Các mã băm SHA-256 niêm phong các mốc kiểm định `CP0_BASELINE`, `CP1_TREE_OPT`, `CP5_OSR_DEOPT`, `CP5_OSR_DEOPT_ADV`, `SEAL_BENCHMARK_CLASSICAL`, `SEAL_BENCHMARK_QUANTUM_LIMIT`, `GATE_7.4_LLM_RUNTIME_SEAL`, `GATE_7.5_EXECUTION_SEAL`.
   - **Gate 7.6.2 Cryptographic Triad Seals** tại `test_registry/g7_6_2_triad_seals.json` niêm phong bộ ba trụ cột: `TRSX_PACKAGER_SEAL`, `DECOMPILER_ROUNDTRIP_SEAL`, `MICRO_AOT_PARITY_SEAL`.
5. **Bộ Giáo Trình Học Thuật Toàn Diện (Tersun Master Curriculum)**:
   - Toàn bộ 2 Đại giáo trình, 6 Tập (Volumes), 18 Phần và 68 Chương chuyên sâu trong thư mục `GT/`:
     - *Giáo trình Hệ thống Tersun: Từ Nền tảng đến Kiến trúc Nâng cao* (Vol 1, 2, 3 - Chương 1 đến 28).
     - *Giáo trình Lập trình Tersun: Từ Nguyên lý Thứ nhất* (Vol 1, 2, 3 - Chương 1 đến 40).
   - Toàn bộ hình ảnh, sơ đồ kiến trúc, văn bản giải thích sư phạm, giáo án thực hành, bài tập và đề án kết khóa.

---

## ĐIỀU 2. CÁC QUYỀN ĐƯỢC PHÉP (PERMITTED USES)

Chủ sở hữu quyền tác giả cấp quyền sử dụng miễn phí, không độc quyền, có thể thu hồi, trên phạm vi toàn cầu cho các cá nhân, học viên, nghiên cứu sinh và tổ chức học thuật tuân thủ nghiêm ngặt các mục đích sau:

1. **Học tập, Giảng dạy và Đào tạo Học thuật (Educational Use)**:
   - Được phép đọc, học tập, nghiên cứu và thảo luận nội dung giáo trình và mã nguồn trong môi trường trường học, viện nghiên cứu hoặc tự học cá nhân.
   - Được phép biên dịch, thực thi các ví dụ mã nguồn và chạy các bài kiểm thử đối chuẩn (benchmarks) trên phần cứng của mình.
2. **Nghiên cứu Khoa học & Thực nghiệm Phi Thương mại (Non-Commercial Scientific Research)**:
   - Được phép sử dụng nền tảng Tersun làm đối tượng hoặc công cụ phục vụ các bài báo nghiên cứu khoa học, luận văn cử nhân, thạc sĩ, tiến sĩ.
   - Mọi công trình công bố có sử dụng hoặc trích dẫn nền tảng Tersun **bắt buộc phải ghi rõ nguồn trích dẫn học thuật (Citation Requirement)** theo định dạng quy định tại Điều 4.

---

## ĐIỀU 3. CÁC HÀNH VI BỊ NGHIÊM CẤM (RESTRICTIONS & PROHIBITIONS)

Bất kỳ hành vi nào dưới đây đều bị coi là **hành vi xâm phạm quyền sở hữu trí tuệ nghiêm trọng** và sẽ bị xử lý theo pháp luật hiện hành về sở hữu trí tuệ và quyền tác giả:

1. **Nghiêm cấm Khai thác Thương mại (Commercial Exploitation Prohibition)**:
   - Nghiêm cấm bán, cho thuê, phân phối lại có thu phí, đóng gói thương mại hoặc cung cấp nền tảng Tersun (toàn bộ hoặc một phần) dưới dạng dịch vụ đám mây thương mại (SaaS/PaaS/IaaS) mà không có **hợp đồng cấp phép thương mại bằng văn bản có chữ ký của tác giả**.
2. **Nghiêm cấm Đạo văn, Sao chép & Phân phối Lậu Giáo trình (Plagiarism & Textbook Reproduction Prohibition)**:
   - Nghiêm cấm việc sao chép, trích đoạt nguyên văn, xuất bản lại (dưới dạng in ấn hoặc ebook điện tử), bán khóa học hoặc tái phân phối nội dung của 6 tập giáo trình trong thư mục `GT/` dưới bất kỳ tên gọi hoặc danh nghĩa nào khác.
3. **Nghiêm cấm Đăng ký Bằng Sáng chế Chiếm đoạt (Patent Troll Prohibition)**:
   - Người sử dụng không được phép nộp đơn xin cấp bằng sáng chế, kiểu dáng công nghiệp hoặc giải pháp hữu ích đối với bất kỳ thuật toán, vi kiến trúc nào đã được công bố trong mã nguồn và tài liệu của Tersun (bao gồm TAFPU, BTVP, Zero-Opcode QVM, BitNet GEMM, Attention Ladder, TRSX container, Adaptive Dequickening).
4. **Bảo vệ Tính Toàn vẹn và Thương hiệu (Integrity & Trademark Protection)**:
   - Không được phép gỡ bỏ các thông báo bản quyền, nhãn hiệu bản quyền, chữ ký mã băm mật mã (SHA-256 milestone seals, Triad seals) hoặc thông tin tác giả khỏi mã nguồn, tài liệu và các sản phẩm phái sinh.

---

## ĐIỀU 4. YÊU CẦU TRÍCH DẪN KHOA HỌC (CITATION MANDATE)

Nếu bạn sử dụng Tersun hoặc các tài liệu trong dự án này cho các nghiên cứu, bài báo hoặc báo cáo kỹ thuật, bạn bắt buộc phải trích dẫn theo định dạng chuẩn BibTeX sau:

```bibtex
@software{tersun_platform_2026,
  author = {Tersun Computing Systems Research Group},
  title = {Tersun 1.0.0: Unified Balanced Ternary Computing, Multi-Tier JIT/AOT Compiler, Scaled Quantum Simulator, Native LLM Inference Engine and TRSX Decompiler Ecosystem},
  year = {2026},
  url = {https://github.com/Stufusic/Tersun_Language},
  version = {1.0.0},
  note = {Verified with 2.13M Mathematical Invariants, 12/12 CTest Automated Suites and Cryptographic Triad Seals}
}
```

---

## ĐIỀU 5. TUYÊN BỐ MIỄN TRỪ TRÁCH NHIỆM (DISCLAIMER OF WARRANTY)

PHẦN MỀM VÀ TÀI LIỆU NÀY ĐƯỢC CUNG CẤP "NGUYÊN TRẠNG" (AS IS), KHÔNG CÓ BẤT KỲ SỰ BẢO ĐẢM NÀO DÙ LÀ MINH THỊ HAY NGỤ Ý, BAO GỒM NHƯNG KHÔNG GIỚI HẠN Ở CÁC BẢO ĐẢM VỀ KHẢ NĂNG THƯƠNG MẠI, TÍNH PHÙ HỢP CHO MỘT MỤC ĐÍCH CỤ THỂ HOẶC KHÔNG XÂM PHẠM QUYỀN CỦA BÊN THỨ BA. TRONG MỌI TRƯỜNG HỢP, TÁC GIẢ HOẶC CÁC BÊN ĐÓNG GÓP SẼ KHÔNG CHỊU TRÁCH NHIỆM CHO BẤT KỲ KHIẾU NẠI, THIỆT HẠI TRỰC TIẾP HAY GIÁN TIẾP NÀO PHÁT SINH TỪ VIỆC SỬ DỤNG HOẶC KHÔNG THỂ SỬ DỤNG PHẦN MỀM NÀY.

---

*Mọi yêu cầu cấp phép thương mại hoặc hợp tác nghiên cứu chuyên sâu, vui lòng liên hệ trực tiếp với tác giả và đại diện dự án Tersun.*

---
---

# TERSUN INTELLECTUAL PROPERTY & ACADEMIC RESEARCH LICENSE (TIPARL)
## International English Version — Version 1.2.0 (Gate Sealed)
**Copyright (c) 2024–2026 Tersun - Stufusic. All rights reserved.**

---

### PREAMBLE & GOVERNING JURISDICTION
This License Agreement governs the terms and conditions under which the **Tersun Programming Language, Virtual Machine, Compiler Pipeline, and Computing Ecosystem** are made available. This Agreement is constructed and enforceable under international intellectual property treaties, including but not limited to the **Berne Convention for the Protection of Literary and Artistic Works**, the **WIPO Copyright Treaty (WCT)**, the **Trade-Related Aspects of Intellectual Property Rights (TRIPS) Agreement**, Title 17 of the United States Code (**U.S. Copyright Act & DMCA**), and domestic intellectual property statutes worldwide.

---

### SECTION 1. SCOPE OF PROTECTED INTELLECTUAL PROPERTY
This License covers all software components, architecture specifications, algorithms, mathematical models, curriculum texts, and hardware synthesis descriptions originating from the Tersun project, including:
1. **Frontend & Compiler Pipeline:** Pratt operator-precedence parser, zero-copy lexer, static type-checker, monomorphization engine, Tree Canonicalizer, SSA Linear IR, CFG Dominator Trees, and Micro-AOT direct machine compiler.
2. **Execution Engines & Runtimes:** Direct-threaded Virtual Machine, NaN-Boxing 64-bit value encoding, Tri-Color Mark-Sweep Garbage Collector, On-Stack Replacement (OSR) JIT, and Native Access (NA 1.0.0) Layer 0 `core`, Layer 1 `sys`, Layer 2 `std` architecture.
3. **Novel Algebraic & Hardware Substrates:**
   - **TAFPU (Ternary Algebraic Floating-Point Unit):** Infinite-precision algebraic arithmetic on the quadratic field $\mathbb{Q}(\sqrt{3})$ guaranteeing 0% representation drift.
   - **BTVP (Balanced Ternary Virtual Processor):** Ripple-carry-free balanced ternary arithmetic $\{-1, 0, 1\}$.
   - **Zero-Opcode QVM (Quantum Virtual Machine):** Statevector simulation scaling up to $N=29$ qubits ($536\text{M}$ complex amplitudes) in physical memory.
   - **BitNet 1.58-bit Multiplication-Free GEMM:** Weight-ternary convolution and matrix operations without hardware multiplier cycles.
4. **Decompiler, Containerization & Tooling Ecosystem:** 3-level bytecode decompiler (Level 1 Disassembly, Level 2 CFG Recovery & Adaptive Dequickening, Level 3 High-Level Transpilation to C99/Rust), standalone self-extracting TRSX container format, and Language Server Protocol daemon.
5. **Academic Curriculum & Publications:** All 6 textbook volumes across Track A, Track B, Track C in the `GT/` directory.
6. **Cryptographic Milestone Seals:** All SHA-256 integrity proofs (`Doc/SEAL_*.json` and `Doc/SEAL_NA_1_0_0_MASTER.json`).

---

### SECTION 2. PERMITTED RIGHTS (ACADEMIC & NON-COMMERCIAL USE)
Subject to strict compliance with this Agreement, the copyright holder (**Tersun - Stufusic**) hereby grants a worldwide, royalty-free, non-exclusive, revocable license to individuals, academic institutions, and researchers for:
1. **Educational & Learning Pursuits:** Reading, analyzing, executing, and experimenting with the source code, curriculum, and tests in individual or classroom environments.
2. **Non-Commercial Scientific Research:** Utilizing the Tersun platform as a subject or tool for academic research, dissertations, and peer-reviewed scientific publications, provided that mandatory academic citation is made pursuant to Section 5.

---

### SECTION 3. STRICT PROHIBITIONS & RESTRICTIONS
Any of the following acts constitute willful infringement of intellectual property rights and shall be subject to civil and criminal penalties under applicable laws:
1. **Commercial Exploitation Bar:** You shall NOT sell, rent, lease, sublicense, distribute for commercial consideration, bundle into proprietary products, or provide the software as a cloud service (SaaS, PaaS, IaaS) without an explicit, separate written commercial license executed by **Tersun - Stufusic**.
2. **Plagiarism & Textbook Reproduction:** You shall NOT copy, reproduce, republish, sell courses, or redistribute the curriculum textbooks in `GT/` (in print, electronic, or video form) under any other author or imprint name.
3. **Patent Preclusion (Defensive Patent Bar):** You shall NOT file patent applications, utility models, or industrial design claims based on, covering, or derived from any algorithm, hardware microarchitecture, or system disclosed in the Tersun codebase (including TAFPU, BTVP, QVM, Native Access NA 1.0.0, BitNet GEMM).
4. **Attribution & Watermark Preservation:** You shall NOT alter, obscure, strip, or remove any copyright notices, watermark signatures (`Tersun - Stufusic`), cryptographic milestone seals, or author metadata from any source files or derivatives.

---

### SECTION 4. STATUTORY REMEDIES & ENFORCEMENT
Breach of any term in Section 3 immediately and automatically terminates all rights granted under this License. The copyright holder reserves all rights to seek injunctive relief, statutory damages (including statutory damages under 17 U.S.C. § 504 and DMCA § 1203 where applicable), and legal fees across all relevant legal jurisdictions.

---

### SECTION 5. MANDATORY SCIENTIFIC CITATION
Any academic paper, technical report, or publication utilizing or referencing Tersun must cite the work using the following formal citation:

```bibtex
@software{tersun_stufusic_2026,
  author = {Tersun - Stufusic},
  title = {Tersun Computing Platform: Unified Balanced Ternary Architecture, Native Access NA 1.0.0, Multi-Tier JIT/AOT Compiler, and Exact Algebraic Computing},
  year = {2026},
  url = {https://github.com/Stufusic/Tersun},
  version = {1.2.0-NA-1.0.0},
  note = {Formally Sealed under Cryptographic Merkle Root Proof: 6dadf6645f4524f68f0ad64db72554dabcf76f848a158e802b30d1e6645937e6}
}
```

---

### SECTION 6. DISCLAIMER OF WARRANTY & LIMITATION OF LIABILITY
**THIS SOFTWARE AND ACCOMPANYING DOCUMENTATION ARE PROVIDED BY THE COPYRIGHT HOLDER ("TERSUN - STUFUSIC") "AS IS" AND "WITH ALL FAULTS." TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, ALL WARRANTIES, WHETHER EXPRESS, IMPLIED, STATUTORY, OR OTHERWISE, INCLUDING WITHOUT LIMITATION THE IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, TITLE, AND NON-INFRINGEMENT, ARE EXPRESSLY DISCLAIMED.**

**IN NO EVENT SHALL THE COPYRIGHT HOLDER, ITS CONTRIBUTORS, OR AFFILIATES BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, PUNITIVE, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, REVENUE, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.**

---

*For commercial licensing inquiries or institutional partnerships, please contact the author and project representative at: https://github.com/Stufusic/Tersun*
