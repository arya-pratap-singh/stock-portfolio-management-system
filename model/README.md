## Installation

Install app the necessary python dependancies for the model and the api. To install the dependacies run the below commands

--for the prediction model

pip install pandas numpy requests yfinance matplotlib seaborn pandas-datareader datetime keras sklearn
pip install -U scikit-learn

--for the api

pip install fastapi pydantic uvicorn gunicorn

## Usage

--To run the api locally on your system, run the command given below inside the directory where you have the model and api files

uvicorn mlapi:app --reload

--to make request to the api use axios,example given below

app.post('/', async(req,res) => {
    try {
        const inputValue = req.body.company_name;
        const postData = {
            company_name: inputValue
          };
        const response = await axios.post('http://localhost:8000/',postData);
        const responseData = response.data.prediction;
        res.render('index', { prediction: responseData });
      } catch (error) {
        console.error(error);
        res.status(500).json({ message: 'Error retrieving data from API' });
      }
});