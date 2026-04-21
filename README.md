# Organic-Compound-Classifier

# layout 
📓 notebooks/
👉 everything you run

🧠 models/
👉 just the neural network definition

📦 data/
👉 never manually edited in Colab after preprocessing

## IR extraction

To rebuild the IR metadata CSV from the JCAMP files in `data/IR`, run:

```bash
python scripts/extract_ir.py --input-dir data/IR --output data/ir_metadata.csv
```
