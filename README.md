# designing-a-social-network-and-newsfeed-system


1. User Post Service
  - Write:
      + Store post for a user.
      + Store comments against a post.
      + Store counters (number of likes, reshares) against a post.
      + Store a list (user Id) of who like the post; the like type can vary (smile, thumbs up, love, laughter).
  - Read:
      + Read all post by user.
      + Read all/paginated comments for a post.
      + Get number of likes for a post.
      + Get a list of users who liked the post.
    
 2. Post workflow orchestration and memory cache
  - Xử lý 1 lượng lớn request khi cache bằng redis, ví dụ mỗi user trung bình có 1000 flowers và hệ thống nhận khoản 100 post per second, số request call redis lên đến 100,000. Tuy niên số lượng post có thể hơn 100, lượng call redis có thể trở thành bottleneck của latency.-> Cách tiếp cận để giải quyết vấn đề này là sử dụng batching requests. Redis pipelining có thể được sử dungh nhiều request cùng, tận dụng lợi ích của request batching và giải quyết bottleneck. Bulk requests có thể song song tốt cho việc tối ưu hóa.
  - Khi 1 user unflow ai đó, thì cache nên updated remove entry ra khỏi cache, việc này nên làm bằng asynchronous, Bất kì thay đổi nào trong graph service database sẽ được xử lý bởi 1  componentns  khác trong kiến trúc và được xử lý trên từng usercase.

3. User timeline service
- 









    
