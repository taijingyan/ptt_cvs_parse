# CVS-reviewer
This is a project that collects convenience store products reviews.

## Code
The parameter is sent by `URL`. (e.g. `herf="products.html?store=711"`)

In `products.html`, the `<script>` is defined at line 21 ~ 67. The script gets the condition (parameter) by the URL and uses it to filter the table contents.
```javascript
$(document).ready(function() {
    // get URL
    const urlParams = new URLSearchParams(window.location.search);
    const store = urlParams.get('store');
    const category = urlParams.get('category');
    var popularity_lower_bound = urlParams.get('popularity_low');
    var popularity_upper_bound = urlParams.get('popularity_high');
    var score_lower_bound = urlParams.get('score_low');
    var score_upper_bound = urlParams.get('score_high');

    // filter by store
    if (store != null) {
        $("#productTable tr").filter(function() {
            row_store = this.cells[2].innerHTML;
            $(this).toggle(row_store == store);
        });
    }
    // filter by category
    else if (category != null) {
        $("#productTable tr").filter(function() {
            row_category = this.cells[3].innerHTML;
            $(this).toggle(row_category == category);
        });
    }
    // filter by popularity
    else if (popularity_lower_bound != null && popularity_upper_bound != null) {
        popularity_lower_bound = parseInt(popularity_lower_bound);
        popularity_upper_bound = parseInt(popularity_upper_bound);
        $("#productTable tr").filter(function() {
            row_popularity = parseInt(this.cells[5].innerHTML);
            $(this).toggle(row_popularity >= popularity_lower_bound && row_popularity < popularity_upper_bound)
        });
    }
    // filter by score
    else if (score_lower_bound != null && score_upper_bound != null) {
        score_lower_bound = parseInt(score_lower_bound);
        score_upper_bound = parseInt(score_upper_bound);
        $("#productTable tr").filter(function() {
            row_score = parseInt(this.cells[4].innerHTML);
            $(this).toggle(row_score >= score_lower_bound && row_score < score_upper_bound)
        });
    }
});
```