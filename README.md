import streamlit as st

import pandas as pd

import numpy as np

import altair as alt

import time

df = pd.DataFrame(
    np.random.randn(200, 3),
    columns=['a', 'b', 'c'])

c = alt.Chart(df).mark_circle().encode(
    x='a', y='b', size='c', color='c', tooltip=['a', 'b', 'c'])

st.write(c)

st.markdown('hello **world**! :white_check_mark:')         #world 着重色，加上特殊符号emoji


st.markdown('Streamlit is **_really_ cool**.')           # really cool 着重色
st.markdown("This text is :red[colored red], and this is **:blue[colored]** and bold.")   #显示带颜色字体
st.markdown(":orange[$\sqrt{x^2+y^2}=1$] is a Pythagorean identity. :pencil:")      #$包含的部分是特殊部分，需要进一步了解

st.title('AAAAAAAAAAAAAAAAAAAAAAAAA !')
st.title('This a another title :white_check_mark:')   #展示大标题


st.header('This is a header')
st.header('A header with _italics_  :blue[colors] and emojis :sunglasses:')  #展示头文字


st.subheader('This is a subheader')
st.subheader('A subheader with _italics_ :blue[colors] and emojis :sunglasses:')   #展示副头文字


st.caption('This is a string that explains something above.')
st.caption('A caption with _italics_ :blue[colors] and emojis :sunglasses:')    #展示小字体的说明



code = '''def hello():
    print("Hello, Streamlit!")'''
st.code(code, language='python')     #展示代码


st.text('This is some text.')    #展示文本


st.latex(r'''
    a + ar + a r^2 + a r^3 + \cdots + a r^{n-1} =
    \sum_{k=0}^{n-1} ar^k =
    a \left(\frac{1-r^{n}}{1-r}\right)
    ''')


st.write("This is some text.")

st.slider("This is a slider", 0, 100, (15, 75))   #滑动条，从1到100，停留的位置在15到75

st.divider()  # 👈 Draws a horizontal rule

st.write("This text is between the horizontal rules.")

st.divider()  # 👈 Another horizontal rule


df = pd.DataFrame(
   np.random.randn(50, 20),
   columns=('col %d' % i for i in range(20)))

st.dataframe(df)  # Same as st.write(df)              #展示dataframe 形式的表格  st.dataframe(data=None, width=None, height=None, *, use_container_width=False)


st.metric(label="Temperature", value="70 °F", delta="1.2 °F",label_visibility = "collapsed")  #st.metric(label, value, delta=None, delta_color="normal", help=None, label_visibility="visible")

col1, col2, col3= st.columns(3)   #按照三列展示数据
col1.metric("Temperature", "70 °F", "1.2 °F")
col2.metric("Wind", "9 mph", "-8%")
col3.metric("Humidity", "86%", "4%")



st.metric(label="Gas price", value=4, delta=-0.5,
    delta_color="inverse")

st.metric(label="Active developers", value=123, delta=123,
    delta_color="normal")   #delta_color = 'normal','inverse','off' 三个选项

chart_data = pd.DataFrame(
    np.random.randn(20, 3),
    columns=['a', 'b', 'c'])

st.line_chart(chart_data,x = 'a',y = 'b')  #st.line_chart(data=None, *, x=None, y=None, width=0, height=0, use_container_width=True)


if st.button('Say hello'):
    st.write('Why hello there')
else:
    st.write('Goodbye')


df = pd.DataFrame(
    [
       {"command": "st.selectbox", "rating": 4, "is_widget": True},
       {"command": "st.balloons", "rating": 5, "is_widget": False},
       {"command": "st.time_input", "rating": 3, "is_widget": True},
   ]
)
edited_df = st.experimental_data_editor(df, num_rows="dynamic")

favorite_command = edited_df.loc[edited_df["rating"].idxmax()]["command"]
st.markdown(f"Your favorite command is **{favorite_command}** 🎈")


progress_text = "Operation in progress. Please wait."
my_bar = st.progress(50, text=progress_text)

for percent_complete in range(10):
    time.sleep(0.5)
    my_bar.progress(percent_complete + 1, text=progress_text)



with st.spinner('Wait for it...'):
    time.sleep(5)
st.success('Done!')




st.balloons()



st.snow()



st.error('This is an error', icon="🚨")


st.info('This is a purely informational message', icon="ℹ️")



st.success('This is a success message!', icon="✅")


name = st.text_input('Name')
if not name:
  st.warning('Please input a name.')
  st.stop()
st.success('Thank you for inputting a name.')
