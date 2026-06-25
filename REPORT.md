# Báo cáo Lab 21: LoRA/QLoRA Fine-tuning

## 1. Kết quả thực nghiệm

Dưới đây là bảng tổng hợp các chỉ số quan trọng:

|   rank |   alpha |   trainable_params |   train_time_min |   peak_vram_gb |   eval_loss |   eval_perplexity |
|-------:|--------:|-------------------:|-----------------:|---------------:|------------:|------------------:|
|      8 |      16 |        1.8432e+06  |          4.25907 |        8.69673 |     1.55769 |           4.74786 |
|     16 |      32 |        3.6864e+06  |          4.5743  |        6.61775 |     1.51608 |           4.55435 |
|     64 |     128 |        1.47456e+07 |          4.23376 |        7.99903 |     1.47681 |           4.37898 |

## 2. Phân tích & Kết luận

- **Hiệu năng:** Rank **r=64** cho chỉ số Perplexity thấp nhất (4.38), cho thấy khả năng học ngôn ngữ tốt nhất trong 3 cấu hình.
- **Tài nguyên:** Rank r=8 tiết kiệm tham số nhất nhưng r=64 cho thấy sự cải thiện rõ rệt về độ chính xác mà vẫn nằm trong giới hạn VRAM của T4.
- **Chi phí:** Tổng chi phí huấn luyện là khoảng $0.08 USD cho ~13.1 phút hoạt động.

**Kết luận:** Với bài toán fine-tune tiếng Việt quy mô nhỏ, rank r=16 hoặc r=64 là lựa chọn tối ưu trên GPU T4.
