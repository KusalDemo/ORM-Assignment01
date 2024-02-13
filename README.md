
# ORM Assignment 01

Answers : 

Q1. 
    
 
        String hql="FROM Book a WHERE a.publicationYear > 2010";
        Query query = session.createQuery(hql);
        List<Book> list = query.list();

        for(Book book : list){
            System.out.println(book.getId() + " " + book.getTitle() + " " + book.getPublicationYear() + " " + book.getPrice() + " " + book.getAuthor().getName());
        }

Q2.

        String hql2="UPDATE Book b SET b.price = b.price / 100 * 110 WHERE b.author.id = :author";
        Query query1 = session.createQuery(hql2);
        query1.setParameter("author",1);
        int isUpdated = query1.executeUpdate();
        System.out.println(isUpdated > 0 ? "Successfully updated" : "not updated");


Q3. 


        String hqlDeleteBooks = "delete from Book b where b.author.id = :authorId";
        Query queryDeleteBooks = session.createQuery(hqlDeleteBooks);
        queryDeleteBooks.setParameter("authorId", 1);
        int deletedBooksCount = queryDeleteBooks.executeUpdate();
        System.out.println("Deleted " + deletedBooksCount + " associated books");

        String hqlDeleteAuthor = "delete from Author a where a.id = :authorId";
        Query queryDeleteAuthor = session.createQuery(hqlDeleteAuthor);
        queryDeleteAuthor.setParameter("authorId", 1);
        int deletedAuthorCount = queryDeleteAuthor.executeUpdate();
        System.out.println(deletedAuthorCount > 0 ? "Author deleted" : "Author not found");



Q4.

        String hql4="SELECT avg(b.price) FROM Book b";
        Query query = session.createQuery(hql4);
        Double singleResult = (Double) query.getSingleResult();
        System.out.println("Average book price : Rs."+singleResult);

Q5. 

        String hql5="SELECT a.name, COUNT(b) FROM Author a LEFT JOIN a.books b GROUP BY a.id";
        Query query = session.createQuery(hql5);
        List<Object[]> list = query.list();

        for(Object[] objects : list){
            System.out.println(objects[0] + " " + objects[1]);
        }

Q6. 

        Query query = session.createQuery("SELECT a.name , b.title FROM Book b JOIN Author a on b.author.id = a.id WHERE a.country = :countryName");
        query.setParameter("countryName", "SRILANKA");
        List<Object[]> list = query.list();

        for(Object[] object:list){
            System.out.println(object[0]+" "+object[1]);
        }

Q7.

        @JoinColumn(name="author_id")
Q8. 

         Query query = session.createQuery("SELECT a.name FROM Author a WHERE ( SELECT COUNT(b.id) FROM Book b WHERE a.id = b.author.id ) > ( SELECT AVG(authorBookCount) FROM ( SELECT COUNT(b.id) AS authorBookCount FROM Book b GROUP BY b.author.id ))");
        List<String> resultList = query.getResultList();

        for (String s : resultList) {
            System.out.println(s);
        }

