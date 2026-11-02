# BERT ve T5: Mimari İnceleme ve Uygulamalar

BERT (Devlin ve ark., 2019) ve T5 (Raffel ve ark., 2020) modellerinin mimarisini ve ön eğitim
hedeflerini önceden eğitilmiş modeller üzerinde inceleyen Jupyter notebook'u.

## İçerik

1. BERT mimarisi: yapılandırma, parametre dağılımı, tensör boyutları
2. Öz-dikkat mekanizmasının elle hesaplanması ve modelle doğrulanması
3. Maskeli dil modellemesi ve çift yönlü bağlam
4. Bağlamsal kelime temsilleri ("çay": akarsu / içecek)
5. T5 mimarisi: encoder, decoder ve paylaşılan gömme
6. Otoregresif çözümleme (greedy decoding) ve `generate()` ile karşılaştırma
7. Span corruption ön eğitim hedefi
8. Metinden metne çok görevli kullanım (T5-Small ve FLAN-T5)

## Kullanılan modeller

| Model | Hugging Face kimliği | Parametre |
| --- | --- | --- |
| BERTurk (BERT-Base, Türkçe) | `dbmdz/bert-base-turkish-cased` | ~110M |
| T5-Small | `google-t5/t5-small` | ~60M |
| FLAN-T5-Base | `google/flan-t5-base` | ~250M |

Modeller ilk çalıştırmada Hugging Face Hub'dan indirilir (toplam ~1.5 GB).

## Kurulum ve çalıştırma

```bash
pip install -r requirements.txt
pip install torch --index-url https://download.pytorch.org/whl/cpu   # yalnızca CPU
jupyter notebook BERT_T5_Mimari_ve_Uygulamalar.ipynb
```

Notebook GPU gerektirmez; CPU üzerinde birkaç dakikada tamamlanır.

Komut satırından çalıştırıp çıktıları dosyaya yazmak için:

```bash
jupyter nbconvert --to notebook --execute --inplace BERT_T5_Mimari_ve_Uygulamalar.ipynb
```

## Test edilen ortam

- Python 3.13, Windows 10
- torch 2.15.0 (CPU), transformers 5.22.1, sentencepiece 0.2.2, matplotlib 3.11.2, ipywidgets 8.1.9

## Notlar

- Model yükleme raporları (`LOAD REPORT`) ve ilerleme çubukları
  `transformers.logging.set_verbosity_error()` ile gizlenmiştir. Raporlardaki `UNEXPECTED` anahtarlar,
  ön eğitim başlıkları kullanılmadan yüklemeden kaynaklanır ve zararsızdır. Bu ayar transformers'ın
  diğer uyarılarını da gizler; hata ayıklarken satırı kaldırın.
- `ipywidgets`, Jupyter içinde `TqdmWarning: IProgress not found` uyarısını önlemek için kurulur.
- Bölüm 8'de FLAN-T5'in bazı yanıtları hatalıdır (ör. "tbilisi"). Bu, Base boyutundaki modelin
  sınırlılığını gösterir; çıktılar düzeltilmemiştir.

## Kaynaklar

- Devlin, J., Chang, M.-W., Lee, K., Toutanova, K. (2019). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. *NAACL-HLT*.
- Raffel, C. ve ark. (2020). Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer. *JMLR*, 21(140).
- Vaswani, A. ve ark. (2017). Attention Is All You Need. *NeurIPS*.
- Chung, H. W. ve ark. (2022). Scaling Instruction-Finetuned Language Models. *arXiv:2210.11416*.
- Schweter, S. (2020). BERTurk: BERT models for Turkish. Zenodo.
