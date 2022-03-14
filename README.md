# Context-api-guide
Learn how to use context api

We create a Pagecontext provider that we will use to wrap our entire application by set a children props inside the pagecontext provider. This means that every element inside the context provider can used the element passed inside the context provider value

<img width="656" alt="Screenshot 2022-03-09 at 23 32 12" src="https://user-images.githubusercontent.com/74420607/157557052-0138ca18-e072-4530-b215-4486da8c3d11.png">

---

Now we can call our context provider inside our app.js file.
In this way every element that is passed inside the context provider as a children will be able to read the value inside the page context provider

<img width="654" alt="Screenshot 2022-03-09 at 23 31 56" src="https://user-images.githubusercontent.com/74420607/157557017-ab6832d9-19d5-421f-8f9b-b0a7842e5bb6.png">

--- 
we just need import the pagecontext from pagecontext.js , deconstruct the values passed on the pagecontext.provider and call the value in our page.
In this way we can pass all the value we need in all the file in our app without need to pass props up and down (props drilling)

<img width="655" alt="Screenshot 2022-03-09 at 23 32 26" src="https://user-images.githubusercontent.com/74420607/157557041-abdfc078-6bc9-4091-9932-357fdfc9ddf5.png">


<hr/>


# ** next js typescript and fetch api ** 
1. first we create a context file
  
  <img width="720" alt="Screenshot 2022-03-14 at 18 10 48" src="https://user-images.githubusercontent.com/74420607/158234671-d68af0c7-cbcd-4634-a431-488b0ad25287.png">
  
  source code = export const ApiContext = createContext();

export  function ApiContextprovider(props){
    const [element,setElement] = useState({});

useEffect(async ()=>{
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    const data = await response.json();

    setElement(data)

},[])

return(
    <ApiContext.Provider value={{element, setElement}}>
        {props.children}
    </ApiContext.Provider>
)
    
}
<hr/>
2. We wrap the main app file  with the created apiContextProvider on context file

  <img width="681" alt="Screenshot 2022-03-14 at 18 12 50" src="https://user-images.githubusercontent.com/74420607/158234994-cc9eb1cb-eb46-4f22-81a2-7021df7c1eb3.png">
  
  source code = function MyApp({ Component, pageProps }: AppProps) {
  return (
    
      <ApiContextprovider>
        <Component {...pageProps} />
      </ApiContextprovider>
    
  )
}

export default MyApp
<hr/>
3. And now we just need to destructure the value we passed in the Apicontext.Provider and usit in within the file

<img width="601" alt="Screenshot 2022-03-14 at 18 15 39" src="https://user-images.githubusercontent.com/74420607/158235440-7380ac69-2e40-4d46-8867-cce0ecbe04ed.png">

source code = const Home: NextPage = () => {

  const { element } = useContext(ApiContext);
  
 console.log(element)
  return (
    <div className={styles.container}>
      {element.map((ele: any)=>{
        return <p>{ele.id}</p>
      })} 
    </div>
  )
}

export default Home
