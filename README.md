# table-printerconst express = require('express');
const app = express();
const path = require('path');

app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));
app.use(express.urlencoded({ extended: true }));

app.get('/', (req, res) => {
    res.render('form', { table: null, tableNumber: null, length: null });
});

app.post('/', (req, res) => {
    const tableNumber = parseInt(req.body.number);
    const length = parseInt(req.body.length);
    const table = [];

    for (let i = 1; i <= length; i++) {
        table.push({
            index: i,
            result: tableNumber * i
        });
    }

    res.render('form', { tableNumber, length, table });
});

app.listen(3000, () => {
    console.log('Server running on http://localhost:3000');
});
