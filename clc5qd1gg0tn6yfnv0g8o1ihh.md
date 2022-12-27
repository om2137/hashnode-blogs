# SearchBar and filter in database in React(Next.Js)

# Introduction

SearchBar in any application is a key component for finding necessary fields from the Database. This searchbar can be easily implemented in react(NextJs) as a reusable component.

In this post, we will explore how we can implement this component along with code sample.

Github repo used is linked below.

GitHub: https://github.com/om2137/GymMgmt

# Explanation

In SearchBar component, we define a search bar with `item` and `onChange` as parameters. Where item contains database contents, onChange will handle changes in input.

SearchBar component have one input as a Search bar and with help on onChange event whenever, there are any changes in search bar(input) result will be displayed below the searchbar. Where it will render the the fields we assigned it where ever the component is called.

We can use this search bar component anywhere in the project. Where it will have two fileds results and onChange.

For onChange we define a function handleChange where, we take database fields and filter through it to get necessary result. Here we take the filtered values and assign it to results parameter of the searchbar component and assign handleChange to onChange in searchbar component.

Similarly we can create filter component. Where we will not render the search results but instead just use the code in handle changes to filter through results.

# Code

```typescript
import { useEffect, useState } from "react";

interface Props<T> {
    results?: T[];
    renderItem: (item: T) => JSX.Element;
    onChange?: React.ChangeEventHandler;
}

const SearchBar = <T extends object>({results =[], renderItem,onChange}: Props<T>): JSX.Element => {
    // result contianer visibility handler
    const [showRes,setShowRes] = useState(false);
    useEffect(() => {
        if(results.length > 0){
            setShowRes(true);
        }else{
            setShowRes(false);
        }
    }, [results]);
  return (
    <div className='flex items-center justify-center'>
        <div className="hidden lg:inline ">
            <input type="text" 
                onChange={onChange}
                className="lg:w-[420px] xl:w-[600px] px-5 py-3 text-lg rounded-2xl border focus:border-2 border-gray-500  focus:border-gray-700 outline-none transition"
                placeholder="Search"
            />
            {/* search results */}
            {showRes && 
                <div 
                    className="lg:w-[400px] xl:w-[580px]  absolute mt-1 w-full text-lg p-2 bg-white rounded-bl rounded-br max-h-64 shadow-xl overflow-y-auto"
                >
                    {
                        results.map((item, index) => {
                            return (
                                <div key={index} className="flex courso-pointer rounded hover:bg-slate-400 hover:bg-opicity-10 p-2" >
                                    {renderItem(item)} 
                                </div>
                            )
                        })
                    }
                </div>
            }
            
        </div>
        <div className="lg:hidden ">
            <input type="text" 
                onChange={onChange}
                className="w-[168px] ml:w-[250px] px-5 py-3 text-lg rounded-2xl border focus:border-2 border-gray-500  focus:border-gray-700 outline-none transition"
                placeholder="Search"
            />
            {/* search results */}
            {showRes && 
                <div 
                    className="w-[200px] ml:w-[250px] absolute mt-1 w-full text-lg p-2 bg-white rounded-bl rounded-br max-h-44 shadow-xl overflow-y-auto"
                >
                    {
                        results.map((item, index) => {
                            return (
                                <div key={index} className="courso-pointer rounded hover:bg-slate-400 hover:bg-opicity-10 p-2">
                                    {renderItem(item)} 
                                </div>
                            )
                        })
                    }
                </div>
            }
        </div>
    </div>
  )
}
export default SearchBar;
```

### Search bar component

```typescript
import { useEffect, useState } from "react";
import MediaCard from "./cards";

interface Props<T> {
    results?: T[];
    onChange?: React.ChangeEventHandler;
}

const FilterCards = <T extends object>({onChange}: Props<T>): JSX.Element => {
    // result contianer visibility handler
    
  return (
    <div className='flex items-center justify-center'>
        <div className="hidden md:inline p-4">
            <input type="text" 
                onChange={onChange}
                className="md:w-[500px] lg:w-[700px] px-5 py-3 text-lg rounded-lg border border-gray-500 focus:border-gray-700 transition"
                placeholder="Filter"
            />
            
        </div>
        <div className="md:hidden p-2 pt-5">
            <input type="text" 
                onChange={onChange}
                className="w-[280px] sm:w-[400px] px-5 py-3 text-sm rounded-lg border border-gray-500 focus:border-gray-700 transition"
                placeholder="Filter"
            />
        </div>
    </div>
  )
}
export default FilterCards;
```

### filter component

```typescript
const handleChange: changeHandler = (e) => {
    const { target } = e;
    if (!target.value.trim()) return setResults([]);

    const filteredValue = schemaName.filter((members: { Firstname: string; Lastname:string; Contact: Number;}) =>   schemaName.name.toLowerCase().startsWith(target.value.toLowerCase()) ||       schemaName.schemaField.toLowerCase().startsWith(target.value.toLowerCase()) 
    );
    setResults(filteredValue);
  };
//call component where you want as follows
<FilterCards results={results} onChange={handleChange} />
```

### Calling in project

# End Credits

Here we have understood and implemented search bar in NextJs. Where we have made a re usable component which we can call in our project to search and filter results.