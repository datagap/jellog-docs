# Paginator

## Introduction

`jellog-paginator` is the jellog tag for pagination. Requires `DataGap.Jellog.AspNetCore.Mvc.UI.Bootstrap.TagHelpers.Pagination.PagerModel` type of model.

Basic usage:

````xml
<jellog-paginator model="Model.PagerModel" show-info="true"></jellog-paginator>
````

Model:

````csharp
using Microsoft.AspNetCore.Mvc.RazorPages;
using DataGap.Jellog.AspNetCore.Mvc.UI.Bootstrap.TagHelpers.Pagination;

namespace DataGap.Jellog.AspNetCore.Mvc.UI.Bootstrap.Demo.Pages.Components
{
    public class PaginatorModel : PageModel
    {
        public PagerModel PagerModel { get; set; }

        public void OnGet(int currentPage, string sort)
        {
            PagerModel = new PagerModel(100, 10, currentPage, 10, "/Components/Paginator", sort);
        }
    }
}
````



## Demo

See the [paginator demo page](https://bootstrap-taghelpers.jellog.io/Components/Paginator) to see it in action.

## Attributes

### model

`DataGap.Jellog.AspNetCore.Mvc.UI.Bootstrap.TagHelpers.Pagination.PagerModel` type of model can be initialized with the following data:

* `totalCount`
* `shownItemsCount`
* `currentPage`
* `pageSize`
* `pageUrl`
* `sort` (default null)

### show-info

A value indicates if an extra information about start, end and total records will be displayed. Should be one of the following values:

* `false` (default value)
* `true`
