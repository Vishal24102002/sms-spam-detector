# sms-spam-detector
data analytics model for spam sms classifier on the basis of the text/ message entered it can classify the ttext spam or non spam messages 

<h3><b> USES </b></h3>
<ul>
  <li>to classify the messages as spam or non-spam</li>
  <li>can be used in other projects using the model</li>
</ul>
<h3>Steps to use model</h3>
<ol>
<li>
<p><b><h5>Step-1</h5></b> Loading important Files/Modules </p>
<pre lang="sh">
    import pickle
    import nltk
    from nltk.corpus import stopwords
    from nltk.stem import PorterStemmer
    import string

    # reading binary file from the model and vectorizer
    tfidf = pickle.load(open('vectorizer.pkl', 'rb'))
    model = pickle.load(open('model.pkl', 'rb'))
</pre>
</li>
  
<li>
<p><b><h5>Step-2</h5></b> sms_text Pre-Processing </p>
<pre lang="sh">
    nltk.download('stopwords')
    ps = PorterStemmer()
    def transform_text(text):
        text = text.lower() #convert the sms_text to lower case 
        text = nltk.word_tokenize(text) #tokenizing the sms_text and creating tokens 
        
        #removing alphanumeric value from the sms_text(lower case)
        text = [word for word in text if word.isalnum()] 
        # removing stopwords and puncuations from the the text  
        text = [word for word in text if word not in stopwords.words('english') and word not in string.punctuation]
        text = [ps.stem(word) for word in text]
        return " ".join(text)
    transformed_sms=transform_text(<input_sms>)
</pre>
<p><b><h5>Step-3</h5></b> Result Generation </p>
<pre lang="sh">
    vector_input = tfidf.transform([transformed_sms])
    result = model.predict(vector_input)[0]
</pre>
</li>
<li>
<p><h5><b>step-4</b><h5> Showing Result</p>
<pre lan="sh">
  accuracy=model.accuracy_score(y_test,result)
  precision=model.precision_score(y_test,result)
</pre>    
</li>
</ol>
