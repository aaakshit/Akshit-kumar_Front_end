# Steel_eye_assignment



1) Explain what the simple LIST component does?
A list component is used to display a collection of items in a structured manner, it can be implemented using HTML and CSS, or through various front-end frameworks like React or Angular. A list component can be customized to include different types of items, such as text, images, or buttons, and can be styled to fit the overall design of a webpage or application.

2) What Problems / Warnings are there with the code?

In WrappedSingleList Item, the onClickHandler props is called wrongly, it should be called as a 
callback to be called when the list item is clicked.
In WrappedSingleListItem proptypes index and isSelected is not assigned as required, all though
it's not a problem but as these two parameter are crucial for proper functioning of code so it's good 
if we add a required flag on them so that programmer don’t miss to pass them.
The setSelectedIndex function is not defined correctly. It should be defined using useState hook. It can be defined like:
const[selectedIndex, setSelectedIndex]=useState(null);
The isSelected prop in the SingleListItem component is not being passed correctly. It can be corrected by: isSelected={selectedIndex === index}
The PropTypes for the items prop in the WrappedListComponent component are not defined correctly. It should be defined like: PropTypes.arrayOf{PropTypes.shape({text: PropTypes.string.isRequired}))




3) Please fix, optimize, and/or modify the component as much as you think is necessary.
 import React, { useState, useEffect, useMemo, memo} from 'react';
 import PropTypes from 'propTypes';

const WrappedSingleListItem = ({
     index, 
      isSelected,
      onClickHandler,
       text,
}) => (
   <li  
        style={{ backgroundColor: isSelected ? 'green' : 'red'}}
        onClick={() => onClickHandler(index)}
    >
        {text}
    </li>
 );

WrappedSingleListItem.propTypes = {
    index : PropTypes.number.isRequired,
    isSelected : PropTypes.bool.isRequired,
    onClickHandler: PropTypes.func.isRequired,
    text: PropTypes.string.isRequired,
};

const singleListItem = memo(WrappedSingleListItem);


const WrappedListComponent = ({ 
     items,
}) => {

const [selectedIndex, setSelectedIndex] = useState(-1);

useEffect(() =>{
    setSelectedIndex(-1);
}, [items]);

const handleClick = index => {
    setSelectedIndex(index);
};

return(
    <ul style={{ textAlign: 'left' }}>
        {items && items.map((item, index) => (
            <singleListItem
            key = {index}
            onClickHandler={() => handleClick(index)}
            text = {item.text}
            index = {index}
            isSelected = {selectedIndex === index}
            />
        ))}
    </ul>
)
};

WrappedListComponent.propTypes = {
        items: PropTypes.arrayOf(
        PropTypes.shape({
            text : PropTypes.string.isRequired,
        })
    ).isRequired,
};

WrappedListComponent.defaultProps = {
    items : [],
 };

const List = memo(WrappedListComponent);

export default List;

name-Akshit Kumar
reg no: 12018106
