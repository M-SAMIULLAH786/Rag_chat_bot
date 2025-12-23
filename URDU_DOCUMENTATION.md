# RAG-Based PDF Chatbot - Urdu Documentation
# راگ پر مبنی PDF چیٹ بوٹ - مکمل اردو دستاویزات

**تخلیق کار:** Muhammad Samiullah  
**پروجیکٹ:** Build an Enhanced RAG-Based Chatbot Using Your Own PDF Files  
**تاریخ:** December 13, 2025

---

## 📋 فہرست

1. [RAG کیا ہے؟](#rag-کیا-ہے)
2. [پروجیکٹ کا تعارف](#پروجیکٹ-کا-تعارف)
3. [بنیادی خصوصیات](#بنیادی-خصوصیات)
4. [چار بہتری کی خصوصیات](#چار-بہتری-کی-خصوصیات)
5. [تکنیکی تفصیلات](#تکنیکی-تفصیلات)
6. [کام کا مکمل طریقہ](#کام-کا-مکمل-طریقہ)
7. [Teacher Evaluation کے سوالات](#teacher-evaluation-کے-سوالات)

---

## RAG کیا ہے?

### آسان الفاظ میں:

**RAG = Retrieval + Augmented + Generation**

یعنی: **تلاش + بہتری + جواب بنانا**

### مکمل تشریح:

RAG ایک جدید AI تکنیک ہے جو دو چیزوں کو ملاتی ہے:

1. **Retrieval (تلاش)**:
   - آپ کے دستاویزات میں سے متعلقہ معلومات ڈھونڈنا
   - مثال: کسی کتاب میں سے وہ صفحات نکالنا جن میں آپ کے سوال کا جواب ہے

2. **Generation (جواب بنانا)**:
   - مل جانے والی معلومات کو استعمال کر کے اچھا جواب لکھنا
   - LLM (Large Language Model) استعمال کرنا

### کیوں ضروری ہے؟

**بغیر RAG کے:**
- LLM صرف اپنی training data سے جواب دیتا ہے
- آپ کے personal documents کے بارے میں کچھ نہیں جانتا
- پرانی معلومات دے سکتا ہے

**RAG کے ساتھ:**
- ✅ آپ کے اپنے PDFs سے جواب دیتا ہے
- ✅ تازہ ترین معلومات استعمال کرتا ہے
- ✅ Source citations دیتا ہے (کون سے صفحے سے معلومات لی)
- ✅ زیادہ accurate اور reliable جوابات

### عملی مثال:

```
بغیر RAG:
سوال: "ہمارے course کا grading policy کیا ہے?"
جواب: "معذرت، مجھے آپ کے specific course کے بارے میں معلومات نہیں"

RAG کے ساتھ:
سوال: "ہمارے course کا grading policy کیا ہے?"
جواب: "آپ کے course میں grading policy یہ ہے: 
- Assignments: 30%
- Midterm: 25%
- Final: 35%
- Project: 10%

📚 Source: Course_Syllabus.pdf (Page 4)"
```

---

## پروجیکٹ کا تعارف

### یہ کیا ہے?

یہ ایک **Intelligent PDF Chatbot** ہے جو:
- آپ کے PDFs پڑھتا ہے
- ان میں سے سوالات کے جوابات ڈھونڈتا ہے
- صحیح source کے ساتھ جواب دیتا ہے

### کیوں بنایا؟

1. **Assignment requirement** پوری کرنے کے لیے
2. Students کو documents میں سے جلدی معلومات ملنے میں مدد
3. Research papers کو سمجھنے میں آسانی
4. Long PDFs کو پڑھنے کی بجائے سوال پوچھ کر جواب ملنا

### کہاں استعمال ہو سکتا ہے?

- 📚 **Students**: Course materials سے سوالات پوچھنا
- 👨‍💼 **Professionals**: Company policies, contracts سمجھنا
- 🔬 **Researchers**: Research papers میں specific information ڈھونڈنا
- 📖 **General**: کسی بھی PDF document کے بارے میں سوالات

---

## بنیادی خصوصیات

Assignment میں جو **Base Requirements** تھیں، وہ سب implement کی ہیں:

### 1. ✅ Multiple PDF Upload
```
کیا ہے: ایک ساتھ کئی PDF files upload کر سکتے ہیں
کیسے: Gradio interface میں file upload component
فائدہ: ایک ساتھ متعدد documents سے search کر سکتے ہیں
```

### 2. ✅ Text Extraction from All Pages
```
کیا ہے: PDF کے ہر صفحے سے text نکالنا
کیسے: PyPDF2 library استعمال کی
فائدہ: پوری document کی معلومات available ہوتی ہے
```

### 3. ✅ Semantic Chunking
```
کیا ہے: بڑے text کو چھوٹے چھوٹے meaningful pieces میں تقسیم کرنا
کیوں: LLM کو context window limit ہوتی ہے، سب کچھ ایک ساتھ نہیں بھیج سکتے
کیسے: LangChain کا RecursiveCharacterTextSplitter استعمال کیا
```

### 4. ✅ Vector Similarity Retrieval
```
کیا ہے: سوال سے سب سے زیادہ ملتے جلتے chunks ڈھونڈنا
کیسے: 
  1. ہر chunk کو embedding (numbers) میں تبدیل کرو
  2. Question کو بھی embedding میں تبدیل کرو
  3. Cosine similarity سے compare کرو
  4. Top-3 سب سے ملتے جلتے chunks چن لو
```

### 5. ✅ GROQ LLM Integration
```
کیا ہے: Powerful AI model استعمال کر کے جوابات generate کرنا
Model: Llama 3.3 70B Versatile
API: GROQ (بہت تیز inference)
Temperature: 0.3 (factual answers کے لیے low temperature)
```

### 6. ✅ Gradio Interface
```
کیا ہے: User-friendly web interface
Features:
  - PDF upload tab
  - Chat interface
  - History export
  - About section
```

---

## چار بہتری کی خصوصیات

Assignment میں **کم از کم 2 enhancements** مانگی گئی تھیں۔  
میں نے **4 enhancements** implement کیں:

---

### Enhancement #1: 🧠 Sentence-Transformers for Embeddings

#### کیا تبدیلی کی؟
**پرانا طریقہ (TF-IDF)** کی بجائے **Sentence-Transformers** استعمال کیا

#### TF-IDF کیا ہے اور کیوں کمزور ہے?

**TF-IDF = Term Frequency - Inverse Document Frequency**

یہ صرف **words کی تعداد** دیکھتا ہے:

```
مثال:
Document: "car automobile vehicle transportation"
Question: "tell me about automobiles"

TF-IDF: صرف "automobile" word match ہوگا
Problem: "car" اور "vehicle" کو nahi samjhega (synonyms ہیں)
```

#### Sentence-Transformers کیا ہے اور کیوں بہتر ہے?

**Semantic Understanding** (معنی کو سمجھنا):

```
مثال:
Document: "car automobile vehicle transportation"
Question: "tell me about automobiles"

Sentence-Transformers: 
- "car" = "automobile" = "vehicle" (سب ایک ہی معنی)
- Synonyms، related words، context سب سمجھتا ہے
```

#### Technical Implementation:

```python
# Model load کرنا
from sentence_transformers import SentenceTransformer
embedding_model = SentenceTransformer('all-MiniLM-L6-v2')

# Text کو numbers (vectors) میں تبدیل کرنا
chunk_embeddings = embedding_model.encode(chunk_texts)
# Result: [0.23, -0.45, 0.67, ...] (384 numbers)

# Question کو بھی encode کرنا
question_embedding = embedding_model.encode([question])

# Similarity calculate کرنا
from sklearn.metrics.pairwise import cosine_similarity
similarities = cosine_similarity(question_embedding, chunk_embeddings)

# Top-3 chunks چننا
top_indices = np.argsort(similarities)[-3:][::-1]
```

#### کیوں یہ model چنا؟

**all-MiniLM-L6-v2**:
- ✅ چھوٹا model (80MB)
- ✅ تیز (fast inference)
- ✅ Accurate (semantic understanding)
- ✅ Multilingual support
- ✅ Free اور open source

#### فوائد:

1. **بہتر Accuracy**: صحیح chunks مل جاتے ہیں
2. **Semantic Search**: معنی کی بنیاد پر search
3. **Synonym Handling**: مترادفات کو پہچانتا ہے
4. **Context Understanding**: جملوں کا context سمجھتا ہے

---

### Enhancement #2: 💬 Conversational Memory

#### کیا تبدیلی کی؟

**Chat history** save کرنا تاکہ bot کو پچھلی بات چیت یاد رہے۔

#### بغیر Conversational Memory:

```
User: "What are the graduation requirements?"
Bot: "You need 120 credits, 3.0 GPA..."

User: "What about the GPA?"
Bot: "Sorry, I don't understand. What GPA are you asking about?"
```

**Problem**: Bot کو پچھلا سوال یاد نہیں!

#### Conversational Memory کے ساتھ:

```
User: "What are the graduation requirements?"
Bot: "You need 120 credits, 3.0 GPA..."

User: "What about the GPA?"
Bot: "For graduation, you need a minimum 3.0 GPA..."
```

**Solution**: Bot کو context ملا کہ "GPA" کا تعلق graduation سے ہے!

#### Technical Implementation:

```python
# Global storage
chat_history = []

# جب user سوال پوچھے
def answer_question(question):
    # 1. Relevant chunks ڈھونڈو
    chunks = retrieve_relevant_chunks(question)
    
    # 2. LLM کو بھیجنے کے لیے messages بناؤ
    messages = [{"role": "system", "content": system_prompt}]
    
    # 3. پچھلی chat history شامل کرو (last 3 Q&A pairs)
    for msg in chat_history[-6:]:  # 3 questions + 3 answers = 6
        messages.append({
            "role": msg["role"],
            "content": msg["content"]
        })
    
    # 4. نیا question شامل کرو
    messages.append({"role": "user", "content": question})
    
    # 5. LLM سے جواب لو
    answer = query_groq(messages)
    
    # 6. History میں save کرو
    chat_history.append({"role": "user", "content": question})
    chat_history.append({"role": "assistant", "content": answer})
    
    return answer
```

#### کیوں صرف last 3 Q&A pairs?

```
Token Limit:
- LLMs کی context window limited ہوتی ہے
- Llama 3.3 70B: ~8000 tokens
- Last 3 exchanges enough context دیتے ہیں
- بہت زیادہ history بھیجنے سے:
  ✗ Slow processing
  ✗ زیادہ tokens = زیادہ cost
  ✗ Context overflow
```

#### فوائد:

1. **Follow-up Questions**: پچھلے سوال سے جڑے سوالات
2. **Natural Conversation**: جیسے انسان سے بات کر رہے ہو
3. **Pronoun Resolution**: "it", "that", "this" کو سمجھنا
4. **Better User Experience**: بار بار repeat نہیں کرنا پڑتا

---

### Enhancement #3: 📍 Source References with Page Numbers

#### کیا تبدیلی کی؟

ہر جواب کے ساتھ **exact source citation** دینا:
- File name
- Page number
- Relevance score

#### کیوں ضروری ہے؟

**Without Sources:**
```
Bot: "The deadline is December 31st"
User thinking: "کہاں لکھا ہے یہ? یقین کیسے کروں?"
```

**With Sources:**
```
Bot: "The deadline is December 31st.

📚 Sources Used:
1. Course_Schedule.pdf (Page 5) - Relevance: 92.3%
2. Important_Dates.pdf (Page 2) - Relevance: 78.5%"

User thinking: "Page 5 پر check کر سکتا ہوں! ✅"
```

#### Technical Implementation:

##### Step 1: Metadata Storage

```python
# جب text extract کرو تو metadata save کرو
def extract_text_from_pdf(pdf_file):
    filename = os.path.basename(pdf_file.name)
    
    for page_num, page in enumerate(pdf_reader.pages, start=1):
        text = page.extract_text()
        
        # Har page ke saath metadata
        pages_data.append({
            "text": text,
            "page": page_num,      # Page number
            "source": filename      # File name
        })
```

##### Step 2: Chunk Level Metadata

```python
# جب chunks بناؤ تو metadata preserve کرو
def chunk_text_with_langchain(pages_data):
    for page_data in pages_data:
        chunks = text_splitter.split_text(page_data["text"])
        
        for chunk_text in chunks:
            document_chunks.append({
                "text": chunk_text,
                "source": page_data["source"],    # File name preserved
                "page": page_data["page"],        # Page number preserved
            })
```

##### Step 3: Retrieval with Metadata

```python
# جب relevant chunks ڈھونڈو تو metadata بھی رکھو
def retrieve_relevant_chunks(question, top_k=3):
    similarities = cosine_similarity(question_embedding, chunk_embeddings)[0]
    top_indices = np.argsort(similarities)[-top_k:][::-1]
    
    relevant_chunks = []
    for idx in top_indices:
        chunk = document_chunks[idx].copy()
        chunk["similarity"] = float(similarities[idx])  # Relevance score
        relevant_chunks.append(chunk)
    
    return relevant_chunks
```

##### Step 4: LLM Prompt with Sources

```python
# LLM کو بھیجتے وقت source information شامل کرو
def query_groq_with_context(question, context_chunks):
    # Context string بناؤ
    context_str = ""
    for i, chunk in enumerate(context_chunks, 1):
        context_str += f"\n[Source {i}: {chunk['source']}, Page {chunk['page']}]\n"
        context_str += f"{chunk['text']}\n"
    
    # System prompt میں citation requirement
    system_prompt = """
    IMPORTANT: Always cite your sources.
    Format: "According to [Source name, Page X], ..."
    """
```

##### Step 5: Display Sources

```python
# جواب کے بعد sources display کرو
def answer_question(question):
    answer = query_groq_with_context(question, relevant_chunks)
    
    # Sources list بناؤ
    sources_text = "\n\n📚 **Sources Used:**\n"
    for i, chunk in enumerate(relevant_chunks, 1):
        sources_text += f"{i}. {chunk['source']} "
        sources_text += f"(Page {chunk['page']}) - "
        sources_text += f"Relevance: {chunk['similarity']:.2%}\n"
    
    full_answer = answer + sources_text
    return full_answer
```

#### Output Example:

```
Question: "What is the grading policy?"

Answer: "According to the course syllabus, the grading policy is:
- Assignments: 30%
- Midterm Exam: 25%
- Final Exam: 35%
- Class Participation: 10%

The grading scale follows the standard university policy with 
A (90-100), B (80-89), C (70-79), D (60-69), and F (below 60).

📚 **Sources Used:**
1. IDS_Course_Syllabus.pdf (Page 4) - Relevance: 94.7%
2. University_Policies.pdf (Page 12) - Relevance: 81.2%
3. IDS_Course_Syllabus.pdf (Page 1) - Relevance: 73.5%"
```

#### فوائد:

1. **Verification**: User خود check کر سکتا ہے
2. **Trust**: AI کے جوابات پر زیادہ اعتماد
3. **Debugging**: غلط جواب ہو تو source دیکھ سکتے ہیں
4. **Academic Integrity**: Proper citations
5. **Transparency**: کہاں سے information آئی

---

### Enhancement #4: ⚙️ Improved Chunking with LangChain

#### کیا تبدیلی کی؟

**Simple splitting** کی بجائے **LangChain's RecursiveCharacterTextSplitter** استعمال کیا۔

#### Simple Splitting کیا ہے؟

```python
# Naive approach
def simple_split(text, chunk_size=500):
    chunks = []
    for i in range(0, len(text), chunk_size):
        chunks.append(text[i:i+chunk_size])
    return chunks
```

**Problem:**
```
Original text:
"...important information about deadlines. The assignment is due on
December 31st. Late submissions will not be accepted..."

Simple split at 500 characters:
Chunk 1: "...important information about deadlines. The assign"
Chunk 2: "ment is due on December 31st. Late submissions will..."
```

**❌ "assignment" word کٹ گیا!**  
**❌ Incomplete sentence**  
**❌ Context بھی ٹوٹ گیا**

#### LangChain RecursiveCharacterTextSplitter کیا ہے؟

**Smart splitting** جو natural boundaries پر text کاٹتا ہے:

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,           # Target size
    chunk_overlap=50,         # Overlap for context
    length_function=len,
    separators=[              # Priority order
        "\n\n",               # 1. Paragraphs (best)
        "\n",                 # 2. Lines
        ".",                  # 3. Sentences
        "!",                  # 4. Exclamations
        "?",                  # 5. Questions
        ",",                  # 6. Clauses
        " ",                  # 7. Words
        ""                    # 8. Characters (last resort)
    ]
)
```

#### کیسے کام کرتا ہے؟

##### Step-by-Step Process:

```
1. Try کرو "\n\n" (paragraphs) سے split:
   - اگر chunks 500 سے چھوٹے ہیں ✅ Done!
   - اگر بڑے ہیں → next separator

2. Try کرو "\n" (lines) سے split:
   - اگر chunks 500 سے چھوٹے ہیں ✅ Done!
   - اگر بڑے ہیں → next separator

3. Try کرو "." (sentences) سے split:
   - اگر chunks 500 سے چھوٹے ہیں ✅ Done!
   - اگر بڑے ہیں → next separator

... اور اسی طرح
```

##### Example:

```
Input text (1500 characters):
"Introduction to Machine Learning

Machine learning is a subset of artificial intelligence. It enables 
computers to learn from data without explicit programming.

There are three main types:
1. Supervised Learning: Uses labeled data
2. Unsupervised Learning: Finds patterns in unlabeled data
3. Reinforcement Learning: Learns through trial and error

Applications include image recognition, natural language processing..."

RecursiveCharacterTextSplitter output:

Chunk 1 (485 chars):
"Introduction to Machine Learning

Machine learning is a subset of artificial intelligence. It enables 
computers to learn from data without explicit programming.

There are three main types:"

Chunk 2 (starting at char 435, overlap 50):
"There are three main types:
1. Supervised Learning: Uses labeled data
2. Unsupervised Learning: Finds patterns in unlabeled data
3. Reinforcement Learning: Learns through trial and error"

Chunk 3 (starting at char 580, overlap 50):
"Reinforcement Learning: Learns through trial and error

Applications include image recognition, natural language processing..."
```

#### Chunk Overlap کیوں؟

```
Without overlap:
Chunk 1: "...The deadline is"
Chunk 2: "December 31st..."

Problem: Context lost! ❌

With 50-char overlap:
Chunk 1: "...important. The deadline is"
Chunk 2: "The deadline is December 31st. Late submissions..."

Solution: Context preserved! ✅
```

#### Configuration Explained:

```python
RecursiveCharacterTextSplitter(
    chunk_size=500,
    # Target size
    # Not strict - can be slightly more or less
    # Flexible to keep sentences complete
    
    chunk_overlap=50,
    # 50 characters overlap between chunks
    # Preserves context at boundaries
    # Trade-off: slight redundancy for better accuracy
    
    length_function=len,
    # How to measure size: character count
    # Alternative: token count (for LLM token limits)
    
    separators=["\n\n", "\n", ".", "!", "?", ",", " ", ""]
    # Priority order for splitting
    # Always tries "better" separators first
)
```

#### فوائد:

1. **Complete Sentences**: جملے ادھورے نہیں کٹتے
2. **Semantic Coherence**: معنی برقرار رہتے ہیں
3. **Context Preservation**: Overlap سے context ٹوٹتا نہیں
4. **Better Retrieval**: Complete chunks = better search
5. **LLM Performance**: پورے sentences سے بہتر جواب

#### Comparison:

| Feature | Simple Split | LangChain Splitter |
|---------|-------------|-------------------|
| Sentence integrity | ❌ Breaks mid-sentence | ✅ Complete sentences |
| Context preservation | ❌ No overlap | ✅ Configurable overlap |
| Semantic coherence | ❌ Random cuts | ✅ Natural boundaries |
| Flexibility | ❌ Fixed size only | ✅ Smart size adjustment |
| Quality | ⭐⭐ | ⭐⭐⭐⭐⭐ |

---

## تکنیکی تفصیلات

### پوری Technology Stack:

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **LLM** | GROQ Llama 3.3 70B | جوابات generate کرنا |
| **Embeddings** | Sentence-Transformers | Semantic search |
| **Chunking** | LangChain | Text splitting |
| **PDF Processing** | PyPDF2 | Text extraction |
| **Similarity** | Scikit-learn | Cosine similarity |
| **UI** | Gradio 4.31.0 | Web interface |
| **Deployment** | Hugging Face Spaces | Cloud hosting |
| **Language** | Python 3.10 | Programming |

---

## کام کا مکمل طریقہ

### Complete Workflow (Step-by-Step):

#### مرحلہ 1: PDF Upload

```
User action: Upload PDF files
↓
System:
1. Gradio file upload component receive کرتا ہے
2. Files کو temporary storage میں save کرتا ہے
3. "Process PDFs" button enable ہو جاتا ہے
```

#### مرحلہ 2: Text Extraction

```python
for pdf_file in uploaded_files:
    pdf_reader = PyPDF2.PdfReader(pdf_file)
    
    for page_num, page in enumerate(pdf_reader.pages, start=1):
        text = page.extract_text()
        
        pages_data.append({
            "text": text,
            "page": page_num,
            "source": filename
        })
```

**Output:** List of pages with metadata

#### مرحلہ 3: Smart Chunking

```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50,
    separators=["\n\n", "\n", ".", " ", ""]
)

for page_data in pages_data:
    chunks = text_splitter.split_text(page_data["text"])
    
    for chunk in chunks:
        document_chunks.append({
            "text": chunk,
            "source": page_data["source"],
            "page": page_data["page"]
        })
```

**Output:** List of semantic chunks with metadata

#### مرحلہ 4: Creating Embeddings

```python
# Load model (happens once at startup)
embedding_model = SentenceTransformer('all-MiniLM-L6-v2')

# Create embeddings for all chunks
chunk_texts = [chunk["text"] for chunk in document_chunks]
chunk_embeddings = embedding_model.encode(
    chunk_texts,
    show_progress_bar=True,
    batch_size=32
)
```

**Output:** Numpy array shape (num_chunks, 384)  
ہر chunk کو 384 numbers میں تبدیل کیا

#### مرحلہ 5: User Asks Question

```
User: "What is the deadline?"
↓
System: Question encode کرتا ہے
↓
question_embedding = embedding_model.encode(["What is the deadline?"])
# Result: Array of 384 numbers
```

#### مرحلہ 6: Finding Relevant Chunks

```python
# Calculate similarity between question and all chunks
similarities = cosine_similarity(
    question_embedding,      # (1, 384)
    chunk_embeddings        # (num_chunks, 384)
)[0]  # Result: (num_chunks,)

# Example output:
# [0.23, 0.89, 0.45, 0.12, 0.78, ...]
#        ^^^^              ^^^^  <-- High similarity!

# Get top-3 chunks
top_indices = np.argsort(similarities)[-3:][::-1]
# Example: [145, 89, 234]

relevant_chunks = []
for idx in top_indices:
    chunk = document_chunks[idx]
    chunk["similarity"] = similarities[idx]
    relevant_chunks.append(chunk)
```

**Output:** Top-3 relevant chunks with scores

#### مرحلہ 7: Preparing LLM Prompt

```python
# Build context string
context_str = ""
for i, chunk in enumerate(relevant_chunks, 1):
    context_str += f"\n[Source {i}: {chunk['source']}, Page {chunk['page']}]\n"
    context_str += f"{chunk['text']}\n"

# Build messages array
messages = [
    {"role": "system", "content": system_prompt},
    
    # Add chat history (last 3 Q&A pairs)
    *chat_history[-6:],
    
    # Add current question with context
    {"role": "user", "content": f"Context:\n{context_str}\n\nQuestion: {question}"}
]
```

#### مرحلہ 8: GROQ API Call

```python
headers = {
    "Authorization": f"Bearer {GROQ_API_KEY}",
    "Content-Type": "application/json"
}

payload = {
    "model": "llama-3.3-70b-versatile",
    "messages": messages,
    "temperature": 0.3,    # Low for factual answers
    "max_tokens": 1024,
    "top_p": 0.9
}

response = requests.post(
    "https://api.groq.com/openai/v1/chat/completions",
    headers=headers,
    json=payload,
    timeout=30
)

if response.status_code == 200:
    answer = response.json()["choices"][0]["message"]["content"]
```

#### مرحلہ 9: Adding Source Citations

```python
sources_text = "\n\n📚 **Sources Used:**\n"
for i, chunk in enumerate(relevant_chunks, 1):
    sources_text += f"{i}. {chunk['source']} "
    sources_text += f"(Page {chunk['page']}) - "
    sources_text += f"Relevance: {chunk['similarity']:.2%}\n"

full_answer = answer + sources_text
```

#### مرحلہ 10: Update Chat History

```python
chat_history.append({
    "role": "user",
    "content": question
})

chat_history.append({
    "role": "assistant",
    "content": answer  # Without sources (for LLM context)
})
```

#### مرحلہ 11: Display to User

```python
# Update Gradio chatbot
history.append((question, full_answer))

return history, ""  # Empty textbox
```

---

### Visual Flow Diagram:

```
┌──────────────────┐
│  User Uploads    │
│   PDF Files      │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  PyPDF2 Extract  │
│  Text + Pages    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   LangChain      │
│  Smart Chunking  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Sentence-Trans   │
│  Create Embed    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Ready for Q&A!  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   User Asks      │
│    Question      │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Encode Question │
│   (Embedding)    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Find Similar    │
│     Chunks       │
│  (Cosine Sim)    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   Top-3 Chunks   │
│   + Metadata     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Build Prompt    │
│  + Chat History  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   GROQ API       │
│  Llama 3.3 70B   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Get Answer      │
│  + Add Sources   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Display to User │
│  + Update History│
└──────────────────┘
```

---

## Teacher Evaluation کے سوالات

### سوال 1: "RAG کیا ہے اور کیوں استعمال کرتے ہیں؟"

**جواب:**

RAG = Retrieval-Augmented Generation

**دو Parts:**
1. **Retrieval**: دستاویزات سے متعلقہ معلومات ڈھونڈنا
2. **Generation**: اُن معلومات سے جواب بنانا

**کیوں ضروری:**
- LLM کو training کے بعد کی معلومات نہیں ملتیں
- Personal documents کے بارے میں کچھ نہیں جانتا
- RAG سے real-time information use ہوتی ہے
- Source citations کے ساتھ accurate جوابات

**مثال:**
```
Without RAG: "Sorry, I don't have access to your documents"
With RAG: "According to page 5 of your syllabus, the deadline is..."
```

---

### سوال 2: "آپ نے کون سے 4 enhancements کیے؟"

**جواب:**

#### 1. Sentence-Transformers Embeddings
- TF-IDF کی بجائے semantic embeddings
- all-MiniLM-L6-v2 model
- Better accuracy

#### 2. Conversational Memory
- Chat history maintenance
- Last 3 Q&A pairs کا context
- Natural follow-up questions

#### 3. Source References
- File name + page number
- Relevance scores
- Verification کے لیے

#### 4. LangChain Chunking
- RecursiveCharacterTextSplitter
- Smart splitting at natural boundaries
- 50-character overlap

---

### سوال 3: "Sentence-Transformers TF-IDF سے کیسے بہتر ہے؟"

**جواب:**

**TF-IDF:**
- Keyword matching
- Word frequency count
- No semantic understanding
- "car" ≠ "automobile"

**Sentence-Transformers:**
- Semantic understanding
- Context aware
- Synonyms recognized
- "car" = "automobile" = "vehicle"

**Example:**
```
Query: "What is the grading policy?"
Document: "Assessment criteria and evaluation method"

TF-IDF: No match (different words)
Sentence-Transformers: High similarity (same meaning!)
```

---

### سوال 4: "Chunking کیوں ضروری ہے؟"

**جواب:**

**Problem:**
- LLMs کی context window limited ہوتی ہے
- Llama 3.3: ~8000 tokens
- پورا PDF نہیں بھیج سکتے

**Solution: Chunking**
- بڑے text کو چھوٹے pieces میں
- صرف relevant chunks بھیجیں
- Less tokens = faster + cheaper

**Why LangChain Splitter:**
- Simple split: جملے کٹ جاتے ہیں
- LangChain: complete sentences
- Overlap: context preserved

---

### سوال 5: "Conversational memory کیسے implement کیا؟"

**جواب:**

**Implementation:**

```python
# Global storage
chat_history = []

# Save every Q&A
chat_history.append({"role": "user", "content": question})
chat_history.append({"role": "assistant", "content": answer})

# Send to LLM (last 3 pairs)
for msg in chat_history[-6:]:
    messages.append(msg)
```

**Why last 3 only:**
- Token limit
- Recent context most important
- 3 pairs = enough context

**Benefit:**
```
Q1: "What is the deadline?"
A1: "December 31st"

Q2: "Can I get an extension?"
A2: [Understands "extension" relates to "deadline"]
```

---

### سوال 6: "Source references کیسے add کیے؟"

**جواب:**

**Process:**

1. **Extraction time**: metadata save
```python
{"text": "...", "source": "file.pdf", "page": 5}
```

2. **Retrieval time**: metadata preserve
```python
relevant_chunks = [...] # with metadata
```

3. **Display time**: format nicely
```python
sources_text = "\n\n📚 Sources:\n"
for chunk in relevant_chunks:
    sources_text += f"{chunk['source']} (Page {chunk['page']})\n"
```

**Output:**
```
📚 Sources Used:
1. Syllabus.pdf (Page 4) - Relevance: 94.7%
2. Schedule.pdf (Page 2) - Relevance: 81.2%
```

---

### سوال 7: "کون سی model استعمال کی؟"

**جواب:**

**LLM Model:**
- Llama 3.3 70B Versatile (GROQ)
- 70 billion parameters
- Very powerful
- Fast inference on GROQ

**Embedding Model:**
- all-MiniLM-L6-v2
- 22 million parameters
- 384-dimensional vectors
- Fast and accurate

**Why these models:**
- Llama 3.3: Best quality answers
- MiniLM: Fast semantic search
- Both: Good balance of speed & quality

---

### سوال 8: "Cosine similarity کیا ہے؟"

**جواب:**

**Simple Explanation:**

دو vectors (number lists) کتنے similar ہیں:

```
Vector 1: [1, 2, 3]
Vector 2: [2, 4, 6]  (same direction, larger)
Cosine similarity = 1.0 (identical)

Vector 1: [1, 0, 0]
Vector 2: [0, 1, 0]  (perpendicular)
Cosine similarity = 0.0 (completely different)

Vector 1: [1, 0, 0]
Vector 2: [-1, 0, 0]  (opposite)
Cosine similarity = -1.0 (opposite)
```

**In our RAG:**
```
Question embedding: [0.23, -0.45, 0.67, ...] (384 numbers)
Chunk embedding:    [0.25, -0.42, 0.70, ...] (384 numbers)

Cosine similarity: 0.94 (94% similar!)
```

**Formula:**
```
similarity = cos(θ) = (A · B) / (||A|| × ||B||)

Where:
- A · B = dot product
- ||A|| = magnitude of A
- θ = angle between vectors
```

---

### سوال 9: "Error handling کیسے کی؟"

**جواب:**

**Multiple levels:**

```python
# 1. API Key Missing
if not GROQ_API_KEY:
    return "⚠️ API key not configured"

# 2. PDF Extraction Errors
try:
    text = extract_pdf(file)
except Exception as e:
    return f"⚠️ Error: {str(e)}"

# 3. Network Errors
try:
    response = requests.post(..., timeout=30)
except requests.Timeout:
    return "⚠️ Request timed out"

# 4. API Errors
if response.status_code != 200:
    return f"⚠️ API Error {response.status_code}"

# 5. No Chunks Found
if not relevant_chunks:
    return "⚠️ No relevant information found"
```

---

### سوال 10: "Deployment کیسے کی؟"

**جواب:**

**Hugging Face Spaces پر:**

1. **Files upload:**
   - app.py
   - requirements.txt
   - README.md

2. **README.md metadata:**
```yaml
---
title: RAG PDF Chatbot
sdk: gradio
sdk_version: 4.31.0
app_file: app.py
---
```

3. **GROQ API Key:**
   - Settings → Repository Secrets
   - Name: GROQ_API_KEY
   - Value: [your key]

4. **Automatic deployment:**
   - HF automatically installs requirements
   - Runs app.py
   - Provides public URL

**Link:** https://huggingface.co/spaces/MSAMI1506/rag-pdf-chatbot

---

### سوال 11: "Performance کیسے optimize کی؟"

**جواب:**

**Optimizations:**

1. **Embeddings caching:**
```python
# Create once, reuse for all queries
chunk_embeddings = embedding_model.encode(chunks)
```

2. **Batch encoding:**
```python
# Encode all chunks together (faster)
embeddings = model.encode(chunks, batch_size=32)
```

3. **Limited context:**
```python
# Only top-3 chunks (not all)
relevant_chunks = get_top_k(similarities, k=3)
```

4. **Chat history limit:**
```python
# Only last 3 Q&A pairs
messages = chat_history[-6:]
```

5. **Low temperature:**
```python
# Faster generation, less randomness
temperature=0.3
```

---

## خلاصہ (Summary)

### کیا بنایا:
✅ RAG-based PDF chatbot with 4 enhancements

### Base Requirements:
✅ Multiple PDF upload  
✅ Text extraction  
✅ Semantic chunking  
✅ Vector similarity  
✅ GROQ LLM integration  
✅ Gradio interface  

### 4 Enhancements:
✅ Sentence-Transformers (vs TF-IDF)  
✅ Conversational memory  
✅ Source references with page numbers  
✅ LangChain smart chunking  

### Technologies:
✅ GROQ Llama 3.3 70B  
✅ Sentence-Transformers  
✅ LangChain  
✅ PyPDF2  
✅ Gradio 4.31.0  
✅ Hugging Face Spaces  

### نتیجہ:
🎯 All requirements met  
🚀 Production-ready deployment  
💯 4 enhancements (exceeds requirement of 2)  
📚 Complete documentation  

---

**تیار کار:** Muhammad Samiullah  
**تاریخ:** December 13, 2025  
**Assignment:** RAG-Based PDF Chatbot  

**شکریہ!** 🙏
