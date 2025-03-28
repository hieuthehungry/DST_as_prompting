# DST_as_prompting
Mã nguồn cho bài mini-project môn Dữ liệu lớn


Các bước thực hiện:
- Tải bộ dữ liệu MultiWOZ về và đặt vào thư mục data, giải nén
- Chạy câu lệnh: pip install -r lib_require.txt
Sau đó thực hiện lần lượt các câu lệnh sau để huấn luyện mô hình và đánh giá:
Ví dụ để huấn luyện mô hình t5-base:

```bash

python data/preprocess_mw22_prompt_by_slot.py data/MultiWOZ_2.2

python run_t5.py --model_name_or_path t5-base --do_train --do_predict --train_file "./data/MultiWOZ_2.2/mw22_prompt_by_slot_train.json" --test_file "./data/MultiWOZ_2.2/mw22_prompt_by_slot_test.json" --output_dir ./exps/t5_base_mw22_prompt_by_slot/ --per_device_train_batch_size 6 --predict_with_generate --text_column="dialogue" --summary_column="state" --save_steps 200000 --overwrite_output_dir --fp16 True

cd data

python postprocess_mw22_prompt_by_slot.py --data_dir ./MultiWOZ_2.2 --out_dir ../exps/t5_base_mw22_prompt_by_slot/dummy/ --test_idx ./MultiWOZ_2.2/mw22_prompt_by_slot_test.idx --prediction_txt ../exps/t5_base_mw22_prompt_by_slot/generated_predictions.txt

cd ..

python eval_mw22_prompt_by_slot.py --data_dir ./data/MultiWOZ_2.2 --prediction_dir ./exps/t5_base_mw22_prompt_by_slot/dummy/  --output_metric_file ./exps/t5_base_mw22_prompt_by_slot/dummy/prediction_score
```

Chi tiết về mã nguồn xem thêm tại file README.md