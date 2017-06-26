## Chapter 1. Lambda Expressions

### 1. Is the comparator code in the Arrays.sort method called in the same thread as the call to sort or a different thread?
The key differences between both the algorithm are as follow :

Arrays.sort() uses single thread and can be much slover for really big arrays

Arrays.parallelSort() uses multiple threads, thus overhead of managing them can decrease performance for small arrays; it should be used for really large arrays

### 2. Using the listFiles(FileFilter) and isDirectory methods of the java.io.File class, write a method that returns all subdirectories of a given directory. Use a lambda expression instead of a FileFilter object. Repeat with a method expression.

```java
public class Test {

    public static void main(String... args) {

        String location = "D:\\";

        File[] dirs_file_filter = new File( location ).listFiles(new FileFilter() {
            @Override
            public boolean accept(File pathname) {
                return  pathname.isDirectory();
            }
        } );

        System.out.println("---------- FileFilter anonymous class -----------------");
        Arrays.stream(dirs_file_filter).forEach(System.out::println);


        File[] dirs_lambda = new File( location ).listFiles( File::isDirectory );

        System.out.println("---------- lambda syntax -----------------");
        Arrays.stream(dirs_lambda).forEach(System.out::println);

        assert Arrays.equals(dirs_file_filter, dirs_lambda);
    }
}
```

### 3. Using the list(FilenameFilter) method of the java.io.File class, write a method that returns all files in a given directory with a given extension. Use a lambda expression, not a FilenameFilter. Which variables from the enclosing scope does it capture?

public class Test {

    public static void main(String... args) {

        String location = "D:\\";
        String extension = "zip";

        final FilenameFilter filter = (File dir, String name ) -> {
            return name.toLowerCase().endsWith( extension );
        };


        String[] fileNames = new File( location ).list( filter );

        Arrays.stream(fileNames).forEach(System.out::println);
    }
}