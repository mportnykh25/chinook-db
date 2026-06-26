import sqlite3
import pandas as pd
import streamlit as st
import plotly.express as px

st.set_page_config(page_title="Music Store Demo", page_icon="🎵", layout="centered")
st.title("🎵 Music Store Analytics")
st.divider()

# your exact same Python code
conn = sqlite3.connect('Chinook_Sqlite.sqlite')
df = pd.read_sql("""
    SELECT g.Name as Genre, COUNT(t.TrackId) as Tracks
    FROM Track t
    JOIN Genre g ON t.GenreId = g.GenreId
    GROUP BY g.Name
    ORDER BY Tracks DESC
    LIMIT 5
""", conn)
conn.close()

# replace print() with Streamlit
st.subheader("Top 5 Genres by Number of Tracks")
st.dataframe(df, hide_index=True)

# add a chart
fig = px.bar(df, x='Genre', y='Tracks',
             color='Tracks',
             color_continuous_scale='Blues',
             template='plotly_white')
st.plotly_chart(fig, use_container_width=True)
