# **Projekt zaliczeniowy – Zastosowania Uczenia Maszynowego**

## **1. Informacje ogólne**
**Nazwa projektu:**  
*Klasyfikacja wiadomości phishingowych*  

**Autor:**  
Konrad Obrębski

**Kierunek, rok i tryb studiów:**  
Informatyka, semestr V  

**Data oddania projektu:**  
13.01.2026

---

## **2. Opis projektu**
Projekt polega na zbudowaniu i porównaniu modeli NLP służących do automatycznej klasyfikacji wiadomości tekstowych jako **spam/phishing** lub **wiadomości normalne (ham)**.  
Celem projektu jest sprawdzenie skuteczności klasycznych metod uczenia maszynowego, sieci neuronowych trenowanych od zera oraz modeli transformerowych w zadaniu detekcji phishingu.  
Projekt może być użyteczny w systemach filtrujących wiadomości SMS lub e-mail w celu zwiększenia bezpieczeństwa użytkowników.

---

## **3. Dane**
**Źródło danych:**  
UCI Machine Learning Repository  

**Link do danych:**  
`https://archive.ics.uci.edu/ml/datasets/sms+spam+collection`  

**Opis danych:**  
- liczba próbek: **5574 wiadomości SMS**  
- liczba cech / kolumn: **2 (tekst wiadomości, etykieta)**  
- format danych: **tekstowy (CSV)**  
- rodzaj etykiet / klas: **binarny – ham (0), spam/phishing (1)**  
- licencja: **do użytku akademickiego (research/education use)**  

**Uwagi:**  
- dane zostały wstępnie oczyszczone (normalizacja tekstu, usunięcie nadmiarowych białych znaków),  
- nie zawierają brakujących wartości,  
- zbiór jest niezbalansowany (klasa spam stanowi mniejszość).

---

## **4. Cel projektu**
Celem projektu jest zbudowanie modelu, który:
- automatycznie klasyfikuje wiadomości tekstowe jako **spam/phishing** lub **wiadomość normalna**,  
- minimalizuje liczbę **false negatives** (przepuszczonych wiadomości phishingowych),  
- umożliwia porównanie skuteczności różnych podejść modelowania tekstu.

Projekt pozwala odpowiedzieć na pytanie, **które podejście NLP najlepiej sprawdza się w detekcji phishingu dla krótkich tekstów**.

---

## **5. Struktura projektu**

| Etap | Nazwa pliku | Opis |
|------|--------------|------|
| 1 | `EDA.ipynb` | Analiza danych, wizualizacje, wnioski |
| 2 | `Baseline_TFIDF.ipynb` | Preprocessing, TF-IDF, modele klasyczne |
| 3 | `NN_From_Scratch.ipynb` | Sieć neuronowa uczona od zera (BiLSTM) |
| 4 | `Transformer_DistilBERT.ipynb` | Fine-tuning modelu transformerowego |
| 5 | `Summary_Comparison.ipynb` | Porównanie modeli i wizualizacja wyników |

---

## **6. Modele**

### **6.1 Model klasyczny ML**
- **Algorytm:** TF-IDF (char n-grams) + LinearSVC  
- **Krótki opis działania:**  
  Tekst reprezentowany jest jako wektor TF-IDF oparty na sekwencjach znaków, a następnie klasyfikowany za pomocą liniowego SVM.  
- **Wyniki / metryki:**  
  - Accuracy: **0.9919**  
  - Macro F1: **0.9821**  

---

### **6.2 Sieć neuronowa zbudowana od zera**
- **Architektura:** Embedding → BiLSTM → Dense  
- **Liczba warstw / neuronów:**  
  - Embedding (128)  
  - BiLSTM (64)  
  - Dense (64)  
- **Funkcje aktywacji i optymalizator:**  
  - ReLU, Sigmoid  
  - Adam  
- **Wyniki:**  
  - Accuracy: **0.9830**  
  - Macro F1: **0.9627**

---

### **6.3 Model transformerowy (fine-tuning)**
- **Nazwa modelu:** DistilBERT (`distilbert-base-uncased`)  
- **Zastosowana biblioteka:** HuggingFace Transformers  
- **Zakres dostosowania:**  
  Fine-tuning całego modelu na zadaniu klasyfikacji binarnej  
- **Wyniki:**  
  - Accuracy: **0.9919**  
  - Macro F1: **0.9824**  
  - Recall (spam): **0.9597**

---

## **7. Ewaluacja**
**Użyte metryki:**  
- Accuracy  
- Precision  
- Recall  
- F1-score  
- Macro F1  

**Porównanie modeli:**

| Model | Metryka główna | Wynik | Uwagi |
|--------|----------------|--------|--------|
| Klasyczny ML | Macro F1 | 0.9821 | Bardzo silny baseline |
| Sieć neuronowa | Macro F1 | 0.9627 | Gorsza generalizacja |
| Transformer | Macro F1 | **0.9824** | Najlepszy recall spam |

**Wizualizacje:**  
- Macierze pomyłek  
- Wykresy porównawcze metryk  
- Learning curves (dla sieci neuronowej)

---

## **8. Wnioski i podsumowanie**
- Najlepsze wyniki uzyskał **model transformerowy (DistilBERT)**.  
- Klasyczny model TF-IDF + SVM okazał się bardzo skuteczny dla krótkich tekstów.  
- Sieć neuronowa trenowana od zera była gorsza z powodu małego zbioru danych i braku pretrainingu.  
- Projekt pokazuje, że **modele wstępnie uczone są najbardziej uniwersalne w zadaniach NLP**.  
- System może być wykorzystany w filtrach anty-phishingowych SMS lub e-mail.

---

## **9. Struktura repozytorium**
```
ZUM_2025_KonradObrebski/
│
├── data/
│ ├── raw/
│ └── processed/
├── notebooks/
│ ├── eda_feature_eng.ipynb
│ ├── classicML_baseline.ipynb
│ ├── NN_From_Scratch.ipynb
│ ├── Transformer.ipynb
│ └── Summary_Comparison.ipynb
├── reports/
├── models/
├── README.md
└── requirements.txt
```

---

## **10. Technologia i biblioteki**
- Python 3.x  
- NumPy, Pandas, Matplotlib  
- scikit-learn  
- TensorFlow  
- PyTorch  
- HuggingFace Transformers  

---

## **11. Licencja projektu**
Projekt udostępniony na licencji:  
**MIT License**

Źródło danych: zgodnie z licencją SMS Spam Collection (UCI).
